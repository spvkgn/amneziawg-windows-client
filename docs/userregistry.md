# Registry Keys for Users

#### `HKCU\Software\AmneziaWG\Language`

When this key is set, the UI will try to use the specified language as display language.
Supported languages: "ca", "cs", "de", "en", "es_ES", "et", "fa", "fi", "fr", "id", "it", "ja", "ko", "nl", "pa_IN", "pl", "pt_BR", "ro", "ru", "si_LK", "sk", "sl", "sv_SE", "tr", "uk", "vi", "zh_CN", "zh_TW".

```
> reg add HKCU\Software\AmneziaWG /v Language /t REG_SZ /d "en" /f
```
