# star_isles_config

Star Isles oyununun **sürüm kontrolü** dosyası. Oyun her açılışta bu deponun
`version.json` dosyasını raw.githubusercontent üzerinden okur ve kendi
derleme numarasıyla (`pubspec.yaml` → `version: <ad>+<kod>`, kod kısmı)
karşılaştırır. Depo **public** olmak zorunda: raw okuma kimlik doğrulamasız.

Okunan adres:
`https://raw.githubusercontent.com/adaonder/star_isles_config/main/version.json`

## Alanlar

| Alan | Anlamı |
|---|---|
| `minVersion` | Derleme numarası bunun **altındaysa** güncelleme **zorunlu**: kapatılamayan diyalog, GÜNCELLE mağazayı açar. |
| `targetVersion` | Bunun altındaysa güncelleme **önerilir**: GÜNCELLE / SONRA, her açılışta bir kez. |
| `infoVersion` | Bunun altındaysa yalnız ana menüdeki sürüm satırı yeni sürümü gösterir; diyalog yok. |
| `versionName` | Diyalog ve menü satırında gösterilen yeni sürüm adı (`1.0.3` gibi). |

Sıra: zorunlu > önerilen > bilgi. Alan yoksa ya da dosya okunamazsa oyun
sessizce "güncel" sayar (ağ hatası oyuncuyu durdurmaz).

## Yeni sürüm çıkarınca

1. Play'de yeni paket **yayına girdikten sonra** (öncesinde oyuncu mağazada
   eski sürümü bulur) `targetVersion` ve `infoVersion`'ı yeni derleme
   numarasına, `versionName`'i yeni ada çek.
2. `minVersion` yalnız eski sürümün **çalışmaması gerekiyorsa** yükseltilir
   (kayıt biçimi değişti, kritik hata). Zorunlu güncelleme oyuncuyu oyuna
   sokmuyor; sık kullanılmaz.
3. Commit + push. Değişiklik oyuna bir sonraki açılışta iner.

Kod tarafı: `star_isles/lib/common/update/update_checker.dart`.
