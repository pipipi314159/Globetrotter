# Globetrotter (TW)

FFXIV Dalamud 插件 **Globetrotter** 的台服（繁中）移植版，自動顯示藏寶圖的寶藏位置。

- 原版：https://github.com/chirpxiv/Globetrotter （作者 Anna，現由 chirp 維護）
- 基於版本：commit `e5ac31b696c599cc00be4d042d12efe53ac3663f`（2025-08-09，v1.2.15，原作者未打 tag）
- Dalamud API：13（Dalamud.NET.Sdk 13.0.0）
- 分支：`tw-api13`

## 功能

- 解讀藏寶圖後自動開啟地圖並插旗（Show on decipher）
- `/tmap`：開啟地圖並在目前藏寶圖的寶藏位置插旗
- 滑鼠懸停在已解讀的藏寶圖上時自動開地圖（Show on hover，預設開啟）
- 打開藏寶圖時改為直接開地圖，取代原本的藏寶圖視窗（Show on open）
- `/pglobetrotter`：開啟設定

## 程式修改

只修改 `Globetrotter/TreasureMaps.cs`：

- 特徵碼改用 `TryScanText` 依序嘗試多組：ShowTreasureMap 先試國際服 7.3 版（`40 84 F6 …`），再試 7.0–7.2 版（`40 84 FF …`）。
- 找不到特徵碼時只停用該功能並寫入警告，不會讓整個插件載入失敗。
- 命中的特徵碼會記錄在 `/xllog`（搜尋 `[TW]`）。

台服實測兩個 hook 都命中原版（7.3）特徵碼，備援目前未使用。

## 台服已確認

- 插件正常載入，ActorControlSelf 與 ShowTreasureMap 兩個 hook 皆成功
- 解讀後自動插旗、`/tmap`、滑鼠懸停、Show on open 皆正常
- 旗子位置與實際寶箱位置一致

## 注意事項

- 若插件在已解讀藏寶圖之後才載入，`/tmap` 第一次可能沒反應；懸停一次藏寶圖或重新登入即可。
- 插件名稱顯示為「Globetrotter (TW)」，但 InternalName 未改，沿用原版設定檔。

## 編譯

```bat
set DALAMUD_HOME=C:\Users\<你的使用者名稱>\AppData\Roaming\FFXIVSimpleLauncher\Dalamud\Injector
dotnet build Globetrotter\Globetrotter.csproj -c Release
```

輸出：`Globetrotter\bin\Release\Globetrotter.dll`

## 作者與授權

原作者 Anna 與維護者 chirp 保有原始程式著作權。原 repo 未附授權檔案；本移植僅供台服玩家使用，如原作者有任何疑慮請聯繫本 repo。

圖示：Map by Adrien Coquet from the Noun Project。

## 問題回報

台服相關問題請回報到本 repo 的 Issues，**請勿回報給原作者**。
