# vue3
曾犯的錯:

1.Dart Sass 3.0.0 後，所有內建函式都會從 `@use "sass:map";` 這類內建模組 (built-in module)，用來操作 SCSS 的 Map (對應 JavaScript 的 Object)的命名空間載入
**在 `.vue` 或 `.scss` 加上 `@use "sass:map";`**
**把 `map-get()` 替換為 `map.get()`**
**`@import`** 已經被淘汰，請使用 **`@use`**

2.靜態資源(例如Json)通常放在 **public**
->放在src/assets會讀不到(我試過了)

3.
