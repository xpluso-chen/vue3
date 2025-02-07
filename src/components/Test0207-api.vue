<template>
    <div>
        <div>
            <span>現在天氣</span>
            <span>{{ airTemperature }}</span>
            <span>°C</span>
        </div>
        <hr>
        <div>{{ countyName }}</div>
    </div>

</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';

// 定義狀態
const airTemperature = ref<string>('?'); // 存儲氣溫
const countyName = ref<string>(''); // 存儲縣市名稱

// 計算經緯度之間的距離 (Haversine formula)
const calculateDistance = (lat1: number, lon1: number, lat2: number, lon2: number): number => {
    const toRad = (value: number): number => (value * Math.PI) / 180;
    const R = 6371; // 地球半徑，單位為公里
    const dLat = toRad(lat2 - lat1);
    const dLon = toRad(lon2 - lon1);
    const a =
        Math.sin(dLat / 2) * Math.sin(dLat / 2) +
        Math.cos(toRad(lat1)) *
        Math.cos(toRad(lat2)) *
        Math.sin(dLon / 2) *
        Math.sin(dLon / 2);
    const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a));
    return R * c; // 回傳距離（公里）
};

// 找到最近的測站
const findClosestStation = async (userLat: number, userLon: number) => {
    const url = `https://opendata.cwa.gov.tw/api/v1/rest/datastore/O-A0003-001?Authorization=CWA-F916FE87-F3F9-4ED1-AF48-2DDF2159AF6F&format=JSON`;

    try {
        const response = await fetch(url);
        const data = await response.json();
        const stations = data.records.Station;
        let closestStation = null;
        let minDistance = Infinity;

        stations.forEach((station: any) => {
            const stationLat = station.GeoInfo.Coordinates[1].StationLatitude;
            const stationLon = station.GeoInfo.Coordinates[1].StationLongitude;
            const distance = calculateDistance(userLat, userLon, stationLat, stationLon);

            if (distance < minDistance) {
                minDistance = distance;
                closestStation = {
                    name: `${station.GeoInfo.CountyName} ,${station.GeoInfo.TownName}`,
                    temperature: Math.round(station.WeatherElement.AirTemperature),
                    distance: minDistance.toFixed(2),
                    obsTime: station.ObsTime.DateTime
                };
            }
        });

        return closestStation;
    } catch (error) {
        console.error('Error fetching weather data:', error);
    }
};

// 找到最近的縣市
const findClosestPosition = async (userLat: number, userLon: number) => {
    const url = '/json/position.json';

    try {
        const response = await fetch(url);
        const data = await response.json();
        const stations = data;
        let closestPosition = null;
        let minDistance = Infinity;

        stations.forEach((station: any) => {
            const stationLat = station.location.lat;
            const stationLon = station.location.lng;
            const distance = calculateDistance(userLat, userLon, stationLat, stationLon);

            if (distance < minDistance) {
                const [city, district] = station.name.split('市');
                minDistance = distance;
                closestPosition = {
                    name: `${city}市,${district}`,
                    distance: minDistance.toFixed(2)
                };
            }
        });

        return closestPosition;
    } catch (error) {
        console.error('Error fetching position data:url錯誤或對方定位沒開', error);
    }
};

// 當頁面載入時觸發的行為
onMounted(() => {
    if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(
            (position) => {
                const userLat = position.coords.latitude;
                const userLon = position.coords.longitude;

                // 找到最近測站並更新畫面
                findClosestStation(userLat, userLon).then((closestStation) => {
                    if (closestStation) {
                        airTemperature.value = closestStation.temperature;//溫度
                    } else {
                        console.log('無法找到離您最近的氣象測站資料');
                    }
                });

                // 找最近的位置和對應的縣市並更新畫面
                findClosestPosition(userLat, userLon).then((closestPosition) => {
                    if (closestPosition) {
                        countyName.value = closestPosition.name;
                    } else {
                        countyName.value = '無法取得您的位置';
                    }
                });
            },
            (error) => {
                console.error('無法取得位置：', error);
                countyName.value = '無法取得您的位置。';
                alert('無法找到離您最近的氣象測站資料，請開啟允許定位。')
            }
        );
    } else {
        alert('您的瀏覽器不支援定位功能。');
    }
});
</script>

<style scoped></style>