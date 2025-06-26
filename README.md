![Build Status](https://github.com/ytdl-org/youtube-dl/workflows/CI/badge.svg)](https://github.com/ytdl-org/youtube-dl/actions?query=workflow%3ACI)

youtube-dl - 從 youtube.com 或其他影片平台下載影片

- [安裝](#安裝)
- [說明](#說明)
- [選項](#選項)
- [配置](#配置)
- [輸出模板](#輸出模板)
- [格式選擇](#格式選擇)
- [影片選擇](#影片選擇)
- [常見問題](#常見問題)
- [開發者說明](#開發者說明)
- [嵌入 YOUTUBE-DL](#嵌入-youtube-dl)
- [錯誤](#錯誤)
- [版權](#版權)

# 安裝

對於所有 UNIX 用戶（Linux、macOS 等），請立即輸入以下內容進行安裝：

    sudo curl -L https://yt-dl.org/downloads/latest/youtube-dl -o /usr/local/bin/youtube-dl
    sudo chmod a+rx /usr/local/bin/youtube-dl

如果您沒有 curl，您可以選擇使用最新的 wget：

    sudo wget https://yt-dl.org/downloads/latest/youtube-dl -O /usr/local/bin/youtube-dl
    sudo chmod a+rx /usr/local/bin/youtube-dl

Windows 用戶可以[下載 .exe 文件](https://yt-dl.org/latest/youtube-dl.exe)並將其放置在其 [PATH](https://en.wikipedia.org/wiki/PATH_%28variable%29) 上的任何位置，但 `%SYSTEMROOT%\System32` 除外（例如，**不要**放在 `C:\Windows\System32` 中）。

您也可以使用 pip：

    sudo -H pip install --upgrade youtube-dl

此命令將更新 youtube-dl（如果您已安裝）。有關更多信息，請參閱 [pypi 頁面](https://pypi.python.org/pypi/youtube_dl)。

macOS 用戶可以使用 [Homebrew](https://brew.sh/) 安裝 youtube-dl：

    brew install youtube-dl

或使用 [MacPorts](https://www.macports.org/)：

    sudo port install youtube-dl

或者，請參閱[開發者說明](#開發者說明)以了解如何檢出和使用 git 儲存庫。有關更多選項，包括 PGP 簽名，請參閱 [youtube-dl 下載頁面](https://ytdl-org.github.io/youtube-dl/download.html)。

# 說明
**youtube-dl** 是一個命令行程序，用於從 YouTube.com 和其他一些網站下載影片。它需要 Python 解釋器，版本 2.6、2.7 或 3.2+，並且不限於特定平台。它應該可以在您的 Unix 機器、Windows 或 macOS 上運行。它已發布到公共領域，這意味著您可以修改、重新分發或以任何您喜歡的方式使用它。

    youtube-dl [選項] URL [URL...]

# 選項
    -h, --help                           打印此幫助文本並退出
    --version                            打印程序版本並退出
    -U, --update                         將此程序更新到最新版本。
                                         確保您有足夠的權限
                                         （如果需要，請使用 sudo 運行）
    -i, --ignore-errors                  繼續下載錯誤，例如
                                         跳過播放列表中不可用的影片
    --abort-on-error                     如果發生錯誤，則中止下載更多影片
                                         （在播放列表或命令行中）
    --dump-user-agent                    顯示當前瀏覽器
                                         識別
    --list-extractors                    列出所有支持的提取器
    --extractor-descriptions             輸出所有支持的提取器的描述
    --force-generic-extractor            強制提取使用通用提取器
    --default-search PREFIX              對不合格的 URL 使用此前綴。
                                         例如 "gvsearch2:" 下載兩個
                                         來自 google 影片的影片，用於 youtube-
                                         dl "large apple"。使用值 "auto"
                                         讓 youtube-dl 猜測（"auto_warning"
                                         在猜測時發出警告）。
                                         "error" 只會拋出錯誤。默認值
                                         "fixup_error" 修復損壞的 URL，但如果
                                         無法修復則發出錯誤，而不是搜索。
    --ignore-config                      不讀取配置文件。當
                                         在全局配置文件中給出時
                                         /etc/youtube-dl.conf：不讀取用戶配置
                                         ~/.config/youtube-dl/config
                                         （Windows 上的 %APPDATA%/youtube-dl/config.txt）
    --config-location PATH               配置文件的位置；
                                         配置的路徑或其包含目錄。
    --flat-playlist                      不提取播放列表中的影片，只列出它們。
    --mark-watched                       將影片標記為已觀看（僅限 YouTube）
    --no-mark-watched                    不將影片標記為已觀看（僅限 YouTube）
    --no-color                           不在輸出中發出顏色代碼

## 網絡選項：
    --proxy URL                          使用指定的 HTTP/HTTPS/SOCKS 代理。
                                         要啟用 SOCKS 代理，請指定一個
                                         適當的方案。例如
                                         socks5://127.0.0.1:1080/。傳入一個
                                         空字符串（--proxy ""）表示直接連接
    --socket-timeout SECONDS             放棄前的等待時間，以秒為單位
    --source-address IP                  要綁定的客戶端 IP 地址
    -4, --force-ipv4                     通過 IPv4 進行所有連接
    -6, --force-ipv6                     通過 IPv6 進行所有連接

## 地理限制：
    --geo-verification-proxy URL         使用此代理驗證某些地理限制網站的 IP 地址。
                                         --proxy 指定的默認代理（或如果選項不存在，則不使用）
                                         用於實際下載。
    --geo-bypass                         通過偽造 X-Forwarded-For HTTP 頭繞過地理限制
    --no-geo-bypass                      不通過偽造 X-Forwarded-For HTTP 頭繞過地理限制
    --geo-bypass-country CODE            強制繞過地理限制，並明確提供兩字母 ISO
                                         3166-2 國家代碼
    --geo-bypass-ip-block IP_BLOCK       強制繞過地理限制，並明確提供 CIDR 表示法的 IP 塊

## 影片選擇：
    --playlist-start NUMBER              播放列表影片從第幾部開始（默認為 1）
    --playlist-end NUMBER                播放列表影片到第幾部結束（默認為最後一部）
    --playlist-items ITEM_SPEC           要下載的播放列表影片項目。
                                         指定播放列表中影片的索引，用逗號分隔，例如：
                                         "--playlist-items 1,2,5,8" 如果您想下載
                                         播放列表中索引為 1、2、5、8 的影片。
                                         您可以指定範圍："--playlist-items 1-3,7,10-13"，
                                         它將下載索引為 1、2、3、7、10、11、12 和 13 的影片。
    --match-title REGEX                  僅下載匹配標題的影片（正則表達式或不區分大小寫的子字符串）
    --reject-title REGEX                 跳過下載匹配標題的影片（正則表達式或不區分大小寫的子字符串）
    --max-downloads NUMBER               下載 NUMBER 個文件後中止
    --min-filesize SIZE                  不下載任何小於 SIZE 的影片（例如 50k 或 44.6m）
    --max-filesize SIZE                  不下載任何大於 SIZE 的影片（例如 50k 或 44.6m）
    --date DATE                          僅下載此日期上傳的影片
    --datebefore DATE                    僅下載此日期或之前上傳的影片（即包含）
    --dateafter DATE                     僅下載此日期或之後上傳的影片（即包含）
    --min-views COUNT                    不下載任何觀看次數少於 COUNT 的影片
    --max-views COUNT                    不下載任何觀看次數多於 COUNT 的影片
    --match-filter FILTER                通用影片過濾器。指定任何鍵
                                         （請參閱“輸出模板”以獲取可用鍵列表）
                                         以匹配鍵是否存在，!key 檢查鍵是否不存在，
                                         key > NUMBER（例如“comment_count > 12”，
                                         也適用於 >=、<、<=、!=、=）與數字比較，
                                         key = 'LITERAL'（例如“uploader = 'Mike Smith'”，
                                         也適用於 !=）與字符串文字匹配，& 要求多個匹配。
                                         未知的值將被排除，除非您在運算符後加上問號（?）。
                                         例如，要僅匹配點贊數超過 100 次且點踩數少於 50 次
                                         （或給定服務不提供點踩功能）的影片，
                                         但同時也有描述的影片，請使用
                                         --match-filter "like_count > 100 &
                                         dislike_count <? 50 & description"。
    --no-playlist                        如果 URL 指向影片和播放列表，則僅下載影片。
    --yes-playlist                       如果 URL 指向影片和播放列表，則下載播放列表。
    --age-limit YEARS                    僅下載適合給定年齡的影片
    --download-archive FILE              僅下載未在存檔文件中列出的影片。
                                         將所有已下載影片的 ID 記錄在其中。
    --include-ads                        同時下載廣告（實驗性）

## 下載選項：
    -r, --limit-rate RATE                每秒最大下載速率（例如 50K 或 4.2M）
    -R, --retries RETRIES                重試次數（默認為 10），或“無限”。
    --fragment-retries RETRIES           片段重試次數（默認為 10），或“無限”（DASH、
                                         hlsnative 和 ISM）
    --skip-unavailable-fragments         跳過不可用的片段（DASH、hlsnative 和 ISM）
    --abort-on-unavailable-fragment      當某些片段不可用時中止下載
    --keep-fragments                     下載完成後將下載的片段保留在磁盤上；
                                         片段默認會被刪除
    --buffer-size SIZE                   下載緩衝區大小（例如 1024 或 16K）（默認為 1024）
    --no-resize-buffer                   不自動調整緩衝區大小。默認情況下，
                                         緩衝區大小會從初始值 SIZE 自動調整。
    --http-chunk-size SIZE               基於塊的 HTTP 下載的塊大小（例如 10485760 或 10M）
                                         （默認為禁用）。可能對繞過網絡服務器施加的帶寬限制有用（實驗性）
    --playlist-reverse                   以相反順序下載播放列表影片
    --playlist-random                    以隨機順序下載播放列表影片
    --xattr-set-filesize                 使用預期文件大小設置文件擴展屬性 ytdl.filesize
    --hls-prefer-native                  使用原生 HLS 下載器而不是 ffmpeg
    --hls-prefer-ffmpeg                  使用 ffmpeg 而不是原生 HLS 下載器
    --hls-use-mpegts                     對 HLS 影片使用 mpegts 容器，
                                         允許在下載時播放影片（某些播放器可能無法播放）
    --external-downloader COMMAND        使用指定的外部下載器。
                                         目前支持 aria2c、avconv、axel、curl、ffmpeg、httpie、wget
    --external-downloader-args ARGS      將這些參數傳遞給外部下載器

## 文件系統選項：
    -a, --batch-file FILE                包含要下載的 URL 的文件（'-' 表示標準輸入），每行一個 URL。
                                         以 '#'、';' 或 ']' 開頭的行被視為註釋並被忽略。
    --id                                 文件名中僅使用影片 ID
    -o, --output TEMPLATE                輸出文件名模板，請參閱“輸出模板”以獲取所有信息
    --output-na-placeholder PLACEHOLDER  輸出文件名模板中不可用元字段的佔位符值
                                         （默認為“NA”）
    --autonumber-start NUMBER            指定 %(autonumber)s 的起始值（默認為 1）
    --restrict-filenames                 將文件名限制為僅 ASCII 字符，並避免文件名中的“&”和空格
    -w, --no-overwrites                  不覆蓋文件
    -c, --continue                       強制恢復部分下載的文件。
                                         默認情況下，youtube-dl 將盡可能恢復下載。
    --no-continue                        不恢復部分下載的文件（從頭開始）
    --no-part                            不使用 .part 文件 - 直接寫入輸出文件
    --no-mtime                           不使用 Last-modified 頭部設置文件修改時間
    --write-description                  將影片描述寫入 .description 文件
    --write-info-json                    將影片元數據寫入 .info.json 文件
    --write-annotations                  將影片註釋寫入 .annotations.xml 文件
    --load-info-json FILE                包含影片信息的 JSON 文件（使用“--write-info-json”選項創建）
    --cookies FILE                       用於讀取 cookie 和轉儲 cookie jar 的文件
    --cache-dir DIR                      youtube-dl 可以永久存儲一些下載信息的
                                         文件系統位置。默認情況下為
                                         $XDG_CACHE_HOME/youtube-dl 或 ~/.cache/youtube-dl。
                                         目前，僅緩存 YouTube 播放器文件（用於帶有混淆簽名的影片），
                                         但這可能會改變。
    --no-cache-dir                       禁用文件系統緩存
    --rm-cache-dir                       刪除所有文件系統緩存文件

## 縮略圖選項：
    --write-thumbnail                    將縮略圖寫入磁盤
    --write-all-thumbnails               將所有縮略圖格式寫入磁盤
    --list-thumbnails                    模擬並列出所有可用的縮略圖格式

## 冗長/模擬選項：
    -q, --quiet                          啟用靜音模式
    --no-warnings                        忽略警告
    -s, --simulate                       不下載影片，也不寫入任何內容到磁盤
    --skip-download                      不下載影片
    -g, --get-url                        模擬，靜音但打印 URL
    -e, --get-title                      模擬，靜音但打印標題
    --get-id                             模擬，靜音但打印 ID
    --get-thumbnail                      模擬，靜音但打印縮略圖 URL
    --get-description                    模擬，靜音但打印影片描述
    --get-duration                       模擬，靜音但打印影片長度
    --get-filename                       模擬，靜音但打印輸出文件名
    --get-format                         模擬，靜音但打印輸出格式
    -j, --dump-json                      模擬，靜音但打印 JSON 信息。
                                         請參閱“輸出模板”以獲取可用鍵的描述。
    -J, --dump-single-json               模擬，靜音但為每個命令行參數打印 JSON 信息。
                                         如果 URL 指向播放列表，則在一行中轉儲整個播放列表信息。
    --print-json                         靜音並將影片信息打印為 JSON（影片仍在下載中）。
    --newline                            將進度條輸出為新行
    --no-progress                        不打印進度條
    --console-title                      在控制台標題欄中顯示進度
    -v, --verbose                        打印各種調試信息
    --dump-pages                         打印使用 base64 編碼的下載頁面以調試問題（非常冗長）
    --write-pages                        將下載的中間頁面寫入當前目錄中的文件以調試問題
    --print-traffic                      顯示發送和讀取的 HTTP 流量
    -C, --call-home                      聯繫 youtube-dl 服務器進行調試
    --no-call-home                       不聯繫 youtube-dl 服務器進行調試

## 解決方法：
    --encoding ENCODING                  強制指定編碼（實驗性）
    --no-check-certificate               抑制 HTTPS 證書驗證
    --prefer-insecure                    使用未加密連接檢索影片信息。
                                         （目前僅支持 YouTube）
    --user-agent UA                      指定自定義用戶代理
    --referer URL                        指定自定義引用者，如果影片訪問受限於一個域，則使用
    --add-header FIELD:VALUE             指定自定義 HTTP 頭部及其值，用冒號“:”分隔。
                                         您可以多次使用此選項
    --bidi-workaround                    解決缺少雙向文本支持的終端。
                                         需要 PATH 中有 bidiv 或 fribidi 可執行文件
    --sleep-interval SECONDS             每次下載前休眠的秒數，單獨使用時或與
                                         --max-sleep-interval 一起使用時，作為隨機休眠範圍的下限
                                         （最小可能休眠秒數）。
    --max-sleep-interval SECONDS         每次下載前隨機休眠範圍的上限
                                         （最大可能休眠秒數）。
                                         必須僅與 --min-sleep-interval 一起使用。

## 影片格式選項：
    -f, --format FORMAT                  影片格式代碼，請參閱“格式選擇”以獲取所有信息
    --all-formats                        下載所有可用的影片格式
    --prefer-free-formats                優先選擇免費影片格式，除非請求特定格式
    -F, --list-formats                   列出請求影片的所有可用格式
    --youtube-skip-dash-manifest         不下載 YouTube 影片的 DASH 清單和相關數據
    --merge-output-format FORMAT         如果需要合併（例如 bestvideo+bestaudio），
                                         則輸出到給定的容器格式。
                                         可以是 mkv、mp4、ogg、webm、flv 之一。
                                         如果不需要合併，則忽略。

## 字幕選項：
    --write-sub                          寫入字幕文件
    --write-auto-sub                     寫入自動生成的字幕文件（僅限 YouTube）
    --all-subs                           下載影片所有可用的字幕
    --list-subs                          列出影片所有可用的字幕
    --sub-format FORMAT                  字幕格式，接受格式偏好，例如：“srt”或“ass/srt/best”
    --sub-lang LANGS                     要下載的字幕語言（可選），用逗號分隔，
                                         使用 --list-subs 獲取可用語言標籤

## 身份驗證選項：
    -u, --username USERNAME              使用此帳戶 ID 登錄
    -p, --password PASSWORD              帳戶密碼。如果省略此選項，youtube-dl 將交互式詢問。
    -2, --twofactor TWOFACTOR            雙因素身份驗證碼
    -n, --netrc                          使用 .netrc 身份驗證數據
    --video-password PASSWORD            影片密碼（vimeo、youku）

## Adobe Pass 選項：
    --ap-mso MSO                         Adobe Pass 多系統運營商（電視提供商）標識符，
                                         使用 --ap-list-mso 獲取可用 MSO 列表
    --ap-username USERNAME               多系統運營商帳戶登錄
    --ap-password PASSWORD               多系統運營商帳戶密碼。如果省略此選項，
                                         youtube-dl 將交互式詢問。
    --ap-list-mso                        列出所有支持的多系統運營商

## 後處理選項：
    -x, --extract-audio                  將影片文件轉換為純音頻文件
                                         （需要 ffmpeg/avconv 和 ffprobe/avprobe）
    --audio-format FORMAT                指定音頻格式：“best”、“aac”、“flac”、“mp3”、“m4a”、“opus”、“vorbis”或“wav”；
                                         默認為“best”；沒有 -x 無效
    --audio-quality QUALITY              指定 ffmpeg/avconv 音頻質量，
                                         對於 VBR 插入 0（更好）到 9（更差）之間的值，
                                         或指定比特率，例如 128K（默認 5）
    --recode-video FORMAT                如有必要，將影片重新編碼為另一種格式
                                         （目前支持：mp4|flv|ogg|webm|mkv|avi）
    --postprocessor-args ARGS            將這些參數傳遞給後處理器
    -k, --keep-video                     後處理後將影片文件保留在磁盤上；
                                         影片默認會被刪除
    --no-post-overwrites                 不覆蓋後處理文件；
                                         後處理文件默認會被覆蓋
    --embed-subs                         將字幕嵌入影片中（僅適用於 mp4、webm 和 mkv 影片）
    --embed-thumbnail                    將縮略圖嵌入音頻作為封面藝術
    --add-metadata                       將元數據寫入影片文件
    --metadata-from-title FORMAT         從影片標題解析額外元數據，例如歌曲標題/藝術家。
                                         格式語法與 --output 相同。
                                         也可以使用帶有命名捕獲組的正則表達式。
                                         解析的參數替換現有值。
                                         示例：--metadata-from-title "%(artist)s - %(title)s"
                                         匹配“Coldplay - Paradise”之類的標題。
                                         示例（正則表達式）：--metadata-from-title "(?P<artist>.+?) - (?P<title>.+)"
    --xattrs                             將元數據寫入影片文件的擴展屬性（使用 dublin core 和 xdg 標準）
    --fixup POLICY                       自動糾正文件的已知錯誤。
                                         可以是 never（什麼都不做）、warn（僅發出警告）、
                                         detect_or_warn（默認；如果可以則修復文件，否則發出警告）
    --prefer-avconv                      優先使用 avconv 而不是 ffmpeg 運行後處理器
    --prefer-ffmpeg                      優先使用 ffmpeg 而不是 avconv 運行後處理器（默認）
    --ffmpeg-location PATH               ffmpeg/avconv 二進制文件的位置；
                                         可以是二進制文件的路徑或其包含目錄。
    --exec CMD                           下載和後處理後對文件執行命令，
                                         類似於 find 的 -exec 語法。
                                         示例：--exec 'adb push {} /sdcard/Music/ && rm {}'
    --convert-subs FORMAT                將字幕轉換為其他格式
                                         （目前支持：srt|ass|vtt|lrc）

# 配置

您可以通過將任何支持的命令行選項放置到配置文件中來配置 youtube-dl。在 Linux 和 macOS 上，系統範圍的配置文件位於 `/etc/youtube-dl.conf`，用戶範圍的配置文件位於 `~/.config/youtube-dl/config`。在 Windows 上，用戶範圍的配置文件位置是 `%APPDATA%\youtube-dl\config.txt` 或 `C:\Users\<user name>\youtube-dl.conf`。請注意，默認情況下配置文件可能不存在，因此您可能需要自己創建它。

例如，使用以下配置文件，youtube-dl 將始終提取音頻，不複製修改時間，使用代理並將所有影片保存在您主目錄的 `Movies` 目錄下：
```
# 以 # 開頭的行是註釋

# 始終提取音頻
-x

# 不複製修改時間
--no-mtime

# 使用此代理
--proxy 127.0.0.1:3128

# 將所有影片保存在您主目錄的 Movies 目錄下
-o ~/Movies/%(title)s.%(ext)s
```

請注意，配置文件中的選項與常規命令行調用中使用的選項（即開關）相同，因此在 `-` 或 `--` 之後**不得有空格**，例如 `-o` 或 `--proxy`，而不是 `- o` 或 `-- proxy`。

如果您想在特定的 youtube-dl 運行中禁用配置文件，可以使用 `--ignore-config`。

如果您想在特定的 youtube-dl 運行中使用自定義配置文件，也可以使用 `--config-location`。

### 使用 `.netrc` 文件進行身份驗證

您可能還希望為支持身份驗證的提取器配置自動憑據存儲（通過使用 `--username` 和 `--password` 提供登錄名和密碼），以便在每次 youtube-dl 執行時不必將憑據作為命令行參數傳遞，並防止在 shell 命令歷史記錄中跟踪明文密碼。您可以使用每個提取器的 [`.netrc` 文件](https://stackoverflow.com/tags/.netrc/info)來實現此目的。為此，您需要在 `$HOME` 中創建一個 `.netrc` 文件，並將權限限制為僅您可讀/寫：
```
touch $HOME/.netrc
chmod a-rwx,u+rw $HOME/.netrc
```
之後，您可以按照以下格式為提取器添加憑據，其中 *extractor* 是提取器的小寫名稱：
```
machine <extractor> login <login> password <password>
```
例如：
```
machine youtube login myaccount@gmail.com password my_youtube_password
machine twitch login my_twitch_account_name password my_twitch_password
```
要使用 `.netrc` 文件激活身份驗證，您應該將 `--netrc` 傳遞給 youtube-dl 或將其放置在[配置文件](#配置)中。

在 Windows 上，您可能還需要手動設置 `%HOME%` 環境變量。例如：
```
set HOME=%USERPROFILE%
```

# 輸出模板

`-o` 選項允許用戶指定輸出文件名的模板。

**簡而言之：**[導航到示例](#輸出模板示例)。

基本用法是在下載單個文件時不設置任何模板參數，例如 `youtube-dl -o funny_video.flv "https://some/video"`。但是，它可能包含特殊序列，這些序列將在下載每個影片時被替換。特殊序列可以根據 [python 字符串格式化操作](https://docs.python.org/2/library/stdtypes.html#string-formatting)進行格式化。例如，`%(NAME)s` 或 `%(NAME)05d`。為了澄清，這是一個百分號，後面跟著括號中的名稱，後面跟著格式化操作。允許的名稱和序列類型是：

 - `id` (字符串)：影片標識符
 - `title` (字符串)：影片標題
 - `url` (字符串)：影片 URL
 - `ext` (字符串)：影片文件名擴展名
 - `alt_title` (字符串)：影片的次要標題
 - `display_id` (字符串)：影片的替代標識符
 - `uploader` (字符串)：影片上傳者的全名
 - `license` (字符串)：影片授權的許可證名稱
 - `creator` (字符串)：影片的創作者
 - `release_date` (字符串)：影片發布日期 (YYYYMMDD)
 - `timestamp` (數字)：影片可用時的 UNIX 時間戳
 - `upload_date` (字符串)：影片上傳日期 (YYYYMMDD)
 - `uploader_id` (字符串)：影片上傳者的暱稱或 ID
 - `channel` (字符串)：影片上傳的頻道全名
 - `channel_id` (字符串)：頻道 ID
 - `location` (字符串)：影片拍攝的實際位置
 - `duration` (數字)：影片長度（秒）
 - `view_count` (數字)：在平台上觀看影片的用戶數量
 - `like_count` (數字)：影片的正面評價數量
 - `dislike_count` (數字)：影片的負面評價數量
 - `repost_count` (數字)：影片的轉發數量
 - `average_rating` (數字)：用戶給出的平均評分，使用的比例取決於網頁
 - `comment_count` (數字)：影片的評論數量
 - `age_limit` (數字)：影片的年齡限制（年）
 - `is_live` (布爾值)：此影片是直播還是固定長度影片
 - `start_time` (數字)：影片應開始播放的時間（秒），如 URL 中指定
 - `end_time` (數字)：影片應結束播放的時間（秒），如 URL 中指定
 - `format` (字符串)：格式的人類可讀描述
 - `format_id` (字符串)：由 `--format` 指定的格式代碼
 - `format_note` (字符串)：有關格式的附加信息
 - `width` (數字)：影片寬度
 - `height` (數字)：影片高度
 - `resolution` (字符串)：寬度和高度的文本描述
 - `tbr` (數字)：音頻和影片的平均比特率（KBit/s）
 - `abr` (數字)：平均音頻比特率（KBit/s）
 - `acodec` (字符串)：使用的音頻編解碼器名稱
 - `asr` (數字)：音頻採樣率（赫茲）
 - `vbr` (數字)：平均影片比特率（KBit/s）
 - `fps` (數字)：幀率
 - `vcodec` (字符串)：使用的影片編解碼器名稱
 - `container` (字符串)：容器格式名稱
 - `filesize` (數字)：如果提前知道，則為字節數
 - `filesize_approx` (數字)：字節數的估計值
 - `protocol` (字符串)：用於實際下載的協議
 - `extractor` (字符串)：提取器名稱
 - `extractor_key` (字符串)：提取器的鍵名
 - `epoch` (數字)：創建文件時的 Unix 紀元時間
 - `autonumber` (數字)：每次下載都會增加的數字，從 `--autonumber-start` 開始
 - `playlist` (字符串)：包含影片的播放列表名稱或 ID
 - `playlist_index` (數字)：影片在播放列表中的索引，根據播放列表的總長度用前導零填充
 - `playlist_id` (字符串)：播放列表標識符
 - `playlist_title` (字符串)：播放列表標題
 - `playlist_uploader` (字符串)：播放列表上傳者的全名
 - `playlist_uploader_id` (字符串)：播放列表上傳者的暱稱或 ID

適用於屬於某些邏輯章節或部分的影片：

 - `chapter` (字符串)：影片所屬章節的名稱或標題
 - `chapter_number` (數字)：影片所屬章節的編號
 - `chapter_id` (字符串)：影片所屬章節的 ID

適用於作為某個系列或節目劇集的影片：

 - `series` (字符串)：影片劇集所屬系列或節目的標題
 - `season` (字符串)：影片劇集所屬季的標題
 - `season_number` (數字)：影片劇集所屬季的編號
 - `season_id` (字符串)：影片劇集所屬季的 ID
 - `episode` (字符串)：影片劇集的標題
 - `episode_number` (數字)：影片劇集在季中的編號
 - `episode_id` (字符串)：影片劇集的 ID

適用於作為音樂專輯的曲目或部分的媒體：

 - `track` (字符串)：曲目標題
 - `track_number` (數字)：曲目在專輯或光盤中的編號
 - `track_id` (字符串)：曲目 ID
 - `artist` (字符串)：曲目的藝術家
 - `genre` (字符串)：曲目的流派
 - `album` (字符串)：曲目所屬專輯的標題
 - `album_type` (字符串)：專輯類型
 - `album_artist` (字符串)：專輯中出現的所有藝術家列表
 - `disc_number` (數字)：曲目所屬光盤或其他物理介質的編號
 - `release_year` (數字)：專輯發行年份 (YYYY)

上述每個序列在輸出模板中引用時，都將替換為與序列名稱對應的實際值。請注意，某些序列不保證存在，因為它們取決於特定提取器獲取的元數據。此類序列將替換為使用 `--output-na-placeholder`（默認為 `NA`）提供的佔位符值。

例如，對於 `-o %(title)s-%(id)s.%(ext)s` 和標題為 `youtube-dl test video` 且 ID 為 `BaW_jenozKcj` 的 mp4 影片，這將導致在當前目錄中創建一個 `youtube-dl test video-BaW_jenozKcj.mp4` 文件。

對於數字序列，您可以使用數字相關的格式化，例如，`%(view_count)05d` 將導致一個字符串，其中觀看次數用零填充到 5 個字符，例如 `00042`。

輸出模板還可以包含任意層次結構路徑，例如 `-o '%(playlist)s/%(playlist_index)s - %(title)s.%(ext)s'`，這將導致在與此路徑模板對應的目錄中下載每個影片。任何缺失的目錄都將自動為您創建。

要在輸出模板中使用百分號文字，請使用 `%%`。要輸出到標準輸出，請使用 `-o -`。

當前默認模板是 `%(title)s-%(id)s.%(ext)s`。

在某些情況下，您不希望出現特殊字符，例如中文、空格或 &，例如在將下載的文件名傳輸到 Windows 系統或通過 8 位不安全通道傳輸文件名時。在這些情況下，添加 `--restrict-filenames` 標誌以獲取較短的標題。

#### 輸出模板和 Windows 批處理文件

如果您在 Windows 批處理文件中使用輸出模板，則必須通過加倍來轉義普通百分號字符 (`%`)，因此 `-o "%(title)s-%(id)s.%(ext)s"` 應變為 `-o "%%(title)s-%%(id)s.%%(ext)s"`。但是，您不應觸摸不是普通字符的 `%`，例如用於擴展的環境變量應保持不變：`-o "C:\%HOMEPATH%\Desktop\%%(title)s.%%(ext)s"`。

#### 輸出模板示例

請注意，在 Windows 上您可能需要使用雙引號而不是單引號。

```bash
$ youtube-dl --get-filename -o '%(title)s.%(ext)s' BaW_jenozKc
youtube-dl test video ''_ä↭𝕐.mp4    # 各種奇怪的字符

$ youtube-dl --get-filename -o '%(title)s.%(ext)s' BaW_jenozKc --restrict-filenames
youtube-dl_test_video_.mp4          # 一個簡單的文件名

# 在單獨的目錄中下載 YouTube 播放列表影片，按播放列表中的影片順序索引
$ youtube-dl -o '%(playlist)s/%(playlist_index)s - %(title)s.%(ext)s' https://www.youtube.com/playlist?list=PLwiyx1dc3P2JR9N8gQaQN_BCvlSlap7re

# 下載 YouTube 頻道/用戶的所有播放列表，將每個播放列表保存在單獨的目錄中：
$ youtube-dl -o '%(uploader)s/%(playlist)s/%(playlist_index)s - %(title)s.%(ext)s' https://www.youtube.com/user/TheLinuxFoundation/playlists

# 下載 Udemy 課程，將每個章節保存在您主目錄下 MyVideos 目錄中的單獨目錄中
$ youtube-dl -u user -p password -o '~/MyVideos/%(playlist)s/%(chapter_number)s - %(chapter)s/%(title)s.%(ext)s' https://www.udemy.com/java-tutorial/

# 下載整個系列季，將每個系列和每個季保存在 C:/MyVideos 下的單獨目錄中
$ youtube-dl -o "C:/MyVideos/%(series)s/%(season_number)s - %(season)s/%(episode_number)s - %(episode)s.%(ext)s" https://videomore.ru/kino_v_detalayah/5_sezon/367617

# 將正在下載的影片流式傳輸到標準輸出
$ youtube-dl -o - BaW_jenozKc
```

# 格式選擇

默認情況下，youtube-dl 會嘗試下載最佳可用質量，即如果您想要最佳質量，則**無需**傳遞任何特殊選項，youtube-dl 會**默認**為您猜測。

但有時您可能希望以不同的格式下載，例如當您的連接速度慢或不穩定時。實現此目的的關鍵機制是所謂的*格式選擇*，您可以根據此機制明確指定所需的格式，根據某些標準選擇格式，設置優先級等等。

格式選擇的通用語法是 `--format FORMAT` 或更短的 `-f FORMAT`，其中 `FORMAT` 是一個*選擇器表達式*，即描述您要下載的格式或格式的表達式。

**簡而言之：**[導航到示例](#格式選擇示例)。

最簡單的情況是請求特定格式，例如使用 `-f 22`，您可以下載格式代碼等於 22 的格式。您可以使用 `--list-formats` 或 `-F` 獲取特定影片的可用格式代碼列表。請注意，這些格式代碼是提取器特定的。

您還可以使用文件擴展名（目前支持 `3gp`、`aac`、`flv`、`m4a`、`mp3`、`mp4`、`ogg`、`wav`、`webm`）來下載作為單個文件提供的特定文件擴展名的最佳質量格式，例如 `-f webm` 將下載作為單個文件提供的 `webm` 擴展名的最佳質量格式。

您還可以使用特殊名稱來選擇特定的邊緣情況格式：

 - `best`：選擇由單個文件表示的最佳質量格式，包含影片和音頻。
 - `worst`：選擇由單個文件表示的最差質量格式，包含影片和音頻。
 - `bestvideo`：選擇最佳質量的純影片格式（例如 DASH 影片）。可能不可用。
 - `worstvideo`：選擇最差質量的純影片格式。可能不可用。
 - `bestaudio`：選擇最佳質量的純音頻格式。可能不可用。
 - `worstaudio`：選擇最差質量的純音頻格式。可能不可用。

例如，要下載最差質量的純影片格式，您可以使用 `-f worstvideo`。

如果您想下載多個影片，並且它們沒有相同的可用格式，您可以使用斜杠指定優先順序。請注意，斜杠是左結合的，即左側的格式優先，例如 `-f 22/17/18` 將下載格式 22（如果可用），否則將下載格式 17（如果可用），否則將下載格式 18（如果可用），否則將抱怨沒有可用的合適格式可供下載。

如果您想下載同一影片的多種格式，請使用逗號作為分隔符，例如 `-f 22,17,18` 將下載所有這三種格式，當然如果它們可用。或者一個更複雜的示例，結合了優先級功能：`-f 136/137/mp4/bestvideo,140/m4a/bestaudio`。

您還可以通過在方括號中放置條件來過濾影片格式，例如 `-f "best[height=720]"`（或 `-f "[filesize>10M]"`）。

以下數字元字段可用於比較 `<`、`<=`、`>`、`>=`、`=`（等於）、`!=`（不等於）：

 - `filesize`：字節數，如果提前知道
 - `width`：影片寬度，如果已知
 - `height`：影片高度，如果已知
 - `tbr`：音頻和影片的平均比特率（KBit/s）
 - `abr`：平均音頻比特率（KBit/s）
 - `vbr`：平均影片比特率（KBit/s）
 - `asr`：音頻採樣率（赫茲）
 - `fps`：幀率

此外，過濾器還適用於 `=`（等於）、`^=`（開頭為）、`$=`（結尾為）、`*=`（包含）以及以下字符串元字段：

 - `ext`：文件擴展名
 - `acodec`：使用的音頻編解碼器名稱
 - `vcodec`：使用的影片編解碼器名稱
 - `container`：容器格式名稱
 - `protocol`：用於實際下載的協議，小寫（`http`、`https`、`rtsp`、`rtmp`、`rtmpe`、`mms`、`f4m`、`ism`、`http_dash_segments`、`m3u8` 或 `m3u8_native`）
 - `format_id`：格式的簡短描述
 - `language`：語言代碼

任何字符串比較都可以加上否定符號 `!` 作為前綴，以產生相反的比較，例如 `!*=`（不包含）。

請注意，上述任何元字段都不保證存在，因為這完全取決於特定提取器獲取的元數據，即影片託管方提供的元數據。

對於值未知格式，除非您在運算符後加上問號 (`?`)，否則將被排除。您可以組合格式過濾器，因此 `-f "[height <=? 720][tbr>500]"` 選擇高達 720p 的影片（或高度未知影片），比特率至少為 500 KBit/s。

您可以使用 `-f <video-format>+<audio-format>` 將兩種格式的影片和音頻合併到一個文件中（需要安裝 ffmpeg 或 avconv），例如 `-f bestvideo+bestaudio` 將分別下載最佳純影片格式和最佳純音頻格式，並使用 ffmpeg/avconv 將它們合併在一起，從而提供最佳整體可用質量。

格式選擇器也可以使用括號分組，例如，如果您想下載高度低於 480 的最佳 mp4 和 webm 格式，可以使用 `-f '(mp4,webm)[height<480]'`。

自 2015 年 4 月底和 2015.04.26 版本以來，youtube-dl 使用 `-f bestvideo+bestaudio/best` 作為默認格式選擇（參見 [#5447](https://github.com/ytdl-org/youtube-dl/issues/5447)、[#5456](https://github.com/ytdl-org/youtube-dl/issues/5456)）。如果安裝了 ffmpeg 或 avconv，這會導致分別下載 `bestvideo` 和 `bestaudio` 並將它們與 ffmpeg/avconv 合併到一個文件中，從而提供最佳整體可用質量。否則，它會回退到 `best`，並導致下載作為單個文件提供的最佳可用質量。對於不來自 YouTube 的影片，也需要 `best`，因為它們不提供兩個不同文件中的音頻和影片。如果您只想下載某些 DASH 格式（例如，如果您對分辨率高於 1080p 的影片不感興趣），您可以將 `-f bestvideo[height<=?1080]+bestaudio/best` 添加到您的配置文件中。請注意，如果您使用 youtube-dl 流式傳輸到 `stdout`（並且很可能將其傳輸到您的媒體播放器），即您明確將輸出模板指定為 `-o -`，youtube-dl 仍使用 `-f best` 格式選擇，以便立即開始向您的播放器傳輸內容，而不是等待 `bestvideo` 和 `bestaudio` 下載並合併。

如果您想保留舊的格式選擇行為（在 youtube-dl 2015.04.26 之前），即您想下載作為單個文件提供的最佳可用質量媒體，您應該使用 `-f best` 明確指定您的選擇。您可能希望將其添加到[配置文件](#配置)中，以便每次運行 youtube-dl 時不必輸入它。

#### 格式選擇示例

請注意，在 Windows 上您可能需要使用雙引號而不是單引號。

```bash
# 下載最佳 mp4 格式，如果沒有 mp4 可用，則下載任何其他最佳格式
$ youtube-dl -f 'bestvideo[ext=mp4]+bestaudio[ext=m4a]/best[ext=mp4]/best'

# 下載最佳可用格式，但不超過 480p
$ youtube-dl -f 'bestvideo[height<=480]+bestaudio/best[height<=480]'

# 下載最佳純影片格式，但不超過 50 MB
$ youtube-dl -f 'best[filesize<50M]'

# 通過 HTTP/HTTPS 協議直接鏈接下載最佳可用格式
$ youtube-dl -f '(bestvideo+bestaudio/best)[protocol^=http]'

# 下載最佳影片格式和最佳音頻格式，不合併它們
$ youtube-dl -f 'bestvideo,bestaudio' -o '%(title)s.f%(format_id)s.%(ext)s'
```
請注意，在最後一個示例中，建議使用輸出模板，因為 bestvideo 和 bestaudio 可能具有相同的文件名。


# 影片選擇

影片可以通過其上傳日期使用 `--date`、`--datebefore` 或 `--dateafter` 選項進行過濾。它們接受兩種格式的日期：

 - 絕對日期：`YYYYMMDD` 格式的日期。
 - 相對日期：`(now|today)[+-][0-9](day|week|month|year)(s)?` 格式的日期。

示例：

```bash
# 僅下載過去 6 個月內上傳的影片
$ youtube-dl --dateafter now-6months

# 僅下載 1970 年 1 月 1 日上傳的影片
$ youtube-dl --date 19700101

$ # 僅下載 200x 年代上傳的影片
$ youtube-dl --dateafter 20000101 --datebefore 20091231
```

# 常見問題

### 如何更新 youtube-dl？

如果您遵循了[我們的手動安裝說明](https://ytdl-org.github.io/youtube-dl/download.html)，您可以簡單地運行 `youtube-dl -U`（或者在 Linux 上，`sudo youtube-dl -U`）。

如果您使用 pip 安裝，只需 `sudo pip install -U youtube-dl` 即可更新。

如果您使用 *apt-get* 或 *yum* 等包管理器安裝了 youtube-dl，請使用標準系統更新機制進行更新。請注意，發行版包通常已過時。根據經驗，youtube-dl 至少每月發布一次，通常每週甚至每天發布。只需訪問 https://yt-dl.org 即可了解當前版本。不幸的是，如果您的發行版提供了一個真正過時的版本，我們 youtube-dl 開發人員無能為力。您可以（也應該）向您的發行版在其錯誤跟踪器或支持論壇中投訴。

作為最後的手段，您還可以卸載由您的包管理器安裝的版本，並遵循我們的手動安裝說明。為此，請刪除發行版的包，例如：

    sudo apt-get remove -y youtube-dl

之後，只需遵循[我們的手動安裝說明](https://ytdl-org.github.io/youtube-dl/download.html)：

```
sudo wget https://yt-dl.org/downloads/latest/youtube-dl -O /usr/local/bin/youtube-dl
sudo chmod a+rx /usr/local/bin/youtube-dl
hash -r
```

再次，從那時起，您將能夠使用 `sudo youtube-dl -U` 進行更新。

### youtube-dl 在 Windows 上啟動極慢

在 Windows Defender 設置中為 `youtube-dl.exe` 添加文件排除。

### 我在 YouTube 播放列表上收到錯誤 `Unable to extract OpenGraph title`

YouTube 在 2014 年 3 月及之後更改了其播放列表格式，因此您至少需要 youtube-dl 2014.07.25 才能下載所有 YouTube 影片。

如果您使用包管理器、pip、setup.py 或 tarball 安裝了 youtube-dl，請使用它們進行更新。請注意，Ubuntu 包似乎不再更新。由於我們與 Ubuntu 沒有關聯，我們無能為力。請隨時向 [Ubuntu 打包人員](mailto:ubuntu-motu@lists.ubuntu.com?subject=outdated%20version%20of%20youtube-dl) [報告錯誤](https://bugs.launchpad.net/ubuntu/+source/youtube-dl/+filebug) - 他們所要做的就是將包更新到一個相對較新的版本。請參閱上面有關更新的方法。

### 我在使用輸出模板時收到錯誤：`error: using output template conflicts with using title, video ID or auto number`

確保您沒有在命令行或配置文件中將 `-o` 與 `-t`、`--title`、`--id`、`-A` 或 `--auto-number` 中的任何一個選項一起使用。如果有的話，請刪除後者。

### 我總是需要傳遞 `-citw` 嗎？

默認情況下，youtube-dl 旨在擁有最佳選項（順便說一句，如果您有令人信服的理由認為這些選項應該不同，[請提交一個問題並解釋](https://yt-dl.org/bug)）。因此，從網頁複製長選項字符串是不必要且有時有害的。特別是，在 `-citw` 中，唯一經常有用的選項是 `-i`。

### 您能把 `-b` 選項放回去嗎？

大多數提出這個問題的人都沒有意識到 youtube-dl 現在默認下載 YouTube 報告的最高可用質量，在某些情況下將是 1080p 或 720p，因此您不再需要 `-b` 選項。對於某些特定影片，YouTube 可能不會報告它們以您感興趣的特定高質量格式可用。在這種情況下，只需使用 `-f` 選項請求它，youtube-dl 將嘗試下載它。

### 我嘗試下載影片時收到 HTTP 錯誤 402。這是什麼？

顯然，如果您下載過多，YouTube 會要求您通過 CAPTCHA 測試。我們正在[考慮提供一種讓您解決 CAPTCHA 的方法](https://github.com/ytdl-org/youtube-dl/issues/154)，但目前，您最好的做法是將網絡瀏覽器指向 YouTube URL，解決 CAPTCHA，然後重新啟動 youtube-dl。

### 我需要其他程序嗎？

youtube-dl 在大多數網站上都能正常運行。但是，如果您想轉換影片/音頻，則需要 [avconv](https://libav.org/) 或 [ffmpeg](https://www.ffmpeg.org/)。在某些網站（最著名的是 YouTube）上，影片可以以更高質量格式檢索，但沒有聲音。youtube-dl 將檢測 avconv/ffmpeg 是否存在，並自動選擇最佳選項。

通過 RTMP 協議流式傳輸的影片或影片格式只有在安裝了 [rtmpdump](https://rtmpdump.mplayerhq.hu/) 後才能下載。下載 MMS 和 RTSP 影片需要安裝 [mplayer](https://mplayerhq.hu/) 或 [mpv](https://mpv.io/)。

### 我下載了影片，但如何播放它？

影片完全下載後，使用任何影片播放器，例如 [mpv](https://mpv.io/)、[vlc](https://www.videolan.org/) 或 [mplayer](https://www.mplayerhq.hu/)。

### 我使用 `-g` 提取了影片 URL，但它無法在另一台機器/我的網絡瀏覽器中播放。

這很大程度上取決於服務。在許多情況下，影片請求（下載/播放）必須來自相同的 IP 地址，並帶有相同的 cookie 和/或 HTTP 頭部。使用 `--cookies` 選項將所需的 cookie 寫入文件，並建議您的下載器從該文件讀取 cookie。某些網站還要求使用通用的用戶代理，使用 `--dump-user-agent` 查看 youtube-dl 中使用的用戶代理。您還可以從使用 `--dump-json` 獲取的 JSON 輸出中獲取必要的 cookie 和 HTTP 頭部。

使用 IPv6 可能會有所幫助；在某些情況下，限制僅適用於 IPv4。某些服務（有時僅適用於部分影片）不限制影片 URL 的 IP 地址、cookie 或用戶代理，但這些是例外而非規則。

請記住，某些 URL 協議**不**受瀏覽器開箱即用支持，包括 RTMP。如果您使用 `-g`，您的下載器也必須支持這些協議。

如果您想在未運行 youtube-dl 的機器上播放影片，您可以從運行 youtube-dl 的機器中轉發影片內容。您可以使用 `-o -` 讓 youtube-dl 將影片流式傳輸到標準輸出，或者簡單地允許播放器依次下載 youtube-dl 寫入的文件。

### 錯誤：在影片信息中找不到 fmt_url_map 或 conn 信息

YouTube 在 2011 年 7 月切換到新的影片信息格式，舊版本的 youtube-dl 不支持該格式。請參閱[上面](#如何更新-youtube-dl)了解如何更新 youtube-dl。

### 錯誤：無法下載影片

YouTube 自 2012 年 9 月起需要額外的簽名，舊版本的 youtube-dl 不支持該簽名。請參閱[上面](#如何更新-youtube-dl)了解如何更新 youtube-dl。

### 影片 URL 包含一個 & 符號，我收到一些奇怪的輸出 `[1] 2839` 或 `'v' 未被識別為內部或外部命令`

這實際上是您的 shell 的輸出。由於 & 符號是特殊 shell 字符之一，它會被 shell 解釋，阻止您將整個 URL 傳遞給 youtube-dl。要禁用您的 shell 解釋 & 符號（或任何其他特殊字符），您必須將整個 URL 放在引號中或用反斜杠轉義它們（哪種方法有效取決於您的 shell）。

例如，如果您的 URL 是 https://www.youtube.com/watch?t=4&v=BaW_jenozKc，您應該得到以下命令：

```youtube-dl 'https://www.youtube.com/watch?t=4&v=BaW_jenozKc'```

或

```youtube-dl https://www.youtube.com/watch?t=4\&v=BaW_jenozKc```

對於 Windows，您必須使用雙引號：

```youtube-dl "https://www.youtube.com/watch?t=4&v=BaW_jenozKc"```

### ExtractorError: Could not find JS function u'OF'

2015 年 2 月，新的 YouTube 播放器在字符串中包含一個字符序列，被舊版本的 youtube-dl 誤解。請參閱[上面](#如何更新-youtube-dl)了解如何更新 youtube-dl。

### HTTP 錯誤 429：請求過多 或 402：需要付款

這兩個錯誤代碼表示服務因過度使用而阻止您的 IP 地址。通常這是一個軟阻止，意味著您在解決 CAPTCHA 後可以再次訪問。只需打開瀏覽器並解決服務建議您的 CAPTCHA，然後將 [cookie 傳遞給 youtube-dl](#如何將-cookie-傳遞給-youtube-dl)。請注意，如果您的機器有多個外部 IP，那麼您還應該傳遞與您用於解決 CAPTCHA 的完全相同的 IP，並使用 [`--source-address`](#網絡選項)。此外，您可能需要使用 [`--user-agent`](#解決方法) 傳遞瀏覽器的 `User-Agent` HTTP 頭部。

如果不是這種情況（服務沒有建議解決 CAPTCHA），那麼您可以聯繫服務並要求他們解除阻止您的 IP 地址，或者 - 如果您已經獲得了白名單 IP 地址 - 使用 [`--proxy` 或 `--source-address` 選項](#網絡選項)選擇另一個 IP 地址。

### SyntaxError: Non-ASCII character

錯誤

    File "youtube-dl", line 2
    SyntaxError: Non-ASCII character '\x93' ...

表示您正在使用過時的 Python 版本。請更新到 Python 2.6 或 2.7。

### 這是什麼二進制文件？代碼去哪兒了？

自 2012 年 6 月以來（[#342](https://github.com/ytdl-org/youtube-dl/issues/342)），youtube-dl 被打包為可執行 zip 文件，只需解壓縮它（在某些系統上可能需要先重命名為 `youtube-dl.zip`）或克隆 git 儲存庫，如上所述。如果您修改代碼，可以通過執行 `__main__.py` 文件來運行它。要重新編譯可執行文件，請運行 `make youtube-dl`。

### exe 由於缺少 `MSVCR100.dll` 而拋出錯誤

要運行 exe，您需要首先安裝 [Microsoft Visual C++ 2010 Service Pack 1 Redistributable Package (x86)](https://download.microsoft.com/download/1/6/5/165255E7-1014-4D0A-B094-B6A430A6BFFC/vcredist_x86.exe)。

### 在 Windows 上，我應該如何設置 ffmpeg 和 youtube-dl？我應該把 exe 文件放在哪裡？

如果您將 youtube-dl 和 ffmpeg 放在您運行命令的同一目錄中，它將會工作，但這相當麻煩。

要使不同的目錄工作 - 無論是 ffmpeg、youtube-dl 還是兩者 - 只需創建目錄（例如，`C:\bin` 或 `C:\Users\<User name>\bin`），將所有可執行文件直接放在其中，然後[設置您的 PATH 環境變量](https://www.java.com/en/download/help/path.xml)以包含該目錄。

從那時起，重新啟動 shell 後，您將能夠通過簡單地輸入 `youtube-dl` 或 `ffmpeg` 來訪問 youtube-dl 和 ffmpeg（並且 youtube-dl 將能夠找到 ffmpeg），無論您身在何處。

### 如何將下載內容放入特定文件夾？

使用 `-o` 指定[輸出模板](#輸出模板)，例如 `-o "/home/user/videos/%(title)s-%(id)s.%(ext)s"`。如果您希望所有下載都這樣，請將該選項放入您的[配置文件](#配置)中。

### 如何下載以 `-` 開頭的影片？

要麼在前面加上 `https://www.youtube.com/watch?v=`，要麼用 `--` 將 ID 與選項分開：

    youtube-dl -- -wNyEUrxzFU
    youtube-dl "https://www.youtube.com/watch?v=-wNyEUrxzFU"

### 如何將 cookie 傳遞給 youtube-dl？

使用 `--cookies` 選項，例如 `--cookies /path/to/cookies/file.txt`。

為了從瀏覽器中提取 cookie，請使用任何符合規範的瀏覽器擴展程序來導出 cookie。例如，[Get cookies.txt LOCALLY](https://chrome.google.com/webstore/detail/get-cookiestxt-locally/cclelndahbckbenkjhflpdbgdldlbecc)（適用於 Chrome）或 [cookies.txt](https://addons.mozilla.org/en-US/firefox/addon/cookies-txt/)（適用於 Firefox）。

請注意，cookie 文件必須是 Mozilla/Netscape 格式，並且 cookie 文件的第一行必須是 `# HTTP Cookie File` 或 `# Netscape HTTP Cookie File`。確保 cookie 文件中的[換行符格式](https://en.wikipedia.org/wiki/Newline)正確，並在必要時將換行符轉換為與您的操作系統對應的格式，即 Windows 為 `CRLF` (`\r\n`)，Unix 和類 Unix 系統（Linux、macOS 等）為 `LF` (`\n`)。使用 `--cookies` 時出現 `HTTP Error 400: Bad Request` 是換行符格式無效的一個好跡象。

將 cookie 傳遞給 youtube-dl 是解決當特定提取器未明確實現登錄時的一種好方法。另一個用例是解決某些網站要求您在特定情況下解決的 [CAPTCHA](https://en.wikipedia.org/wiki/CAPTCHA) 以獲取訪問權限（例如 YouTube、CloudFlare）。

### 如何直接流式傳輸到媒體播放器？

您首先需要告訴 youtube-dl 使用 `-o -` 將媒體流式傳輸到標準輸出，然後告訴您的媒體播放器從標準輸入讀取（它必須能夠這樣做才能進行流式傳輸），然後將前者傳輸給後者。例如，流式傳輸到 [vlc](https://www.videolan.org/) 可以通過以下方式實現：

    youtube-dl -o - "https://www.youtube.com/watch?v=BaW_jenozKcj" | vlc -

### 如何只從播放列表中下載新影片？

使用下載存檔功能。使用此功能，您應該首先使用 `--download-archive /path/to/download/archive/file.txt` 下載完整的播放列表，這將在一個特殊文件中記錄所有影片的標識符。隨後每次使用相同的 `--download-archive` 運行時，將只下載新影片並跳過所有以前下載過的影片。請注意，文件中只記錄成功下載的影片。

例如，首先，

    youtube-dl --download-archive archive.txt "https://www.youtube.com/playlist?list=PLwiyx1dc3P2JR9N8gQaQN_BCvlSlap7re"

將下載完整的 `PLwiyx1dc3P2JR9N8gQaQN_BCvlSlap7re` 播放列表並創建一個 `archive.txt` 文件。隨後每次運行將只下載新影片（如果有的話）：

    youtube-dl --download-archive archive.txt "https://www.youtube.com/playlist?list=PLwiyx1dc3P2JR9N8gQaQN_BCvlSlap7re"

### 我應該將 `--hls-prefer-native` 添加到我的配置中嗎？

當 youtube-dl 檢測到 HLS 影片時，它可以使用內置下載器或 ffmpeg 下載。由於許多 HLS 流略有問題，並且 ffmpeg/youtube-dl 各自處理某些問題情況比對方更好，因此有一個選項可以在需要時切換下載器。

當 youtube-dl 知道某個特定下載器對給定網站效果更好時，將選擇該下載器。否則，youtube-dl 將選擇通用兼容性最佳的下載器，目前恰好是 ffmpeg。此選擇可能會在 youtube-dl 的未來版本中更改，隨著內置下載器和/或 ffmpeg 的改進。

特別是，通用提取器（當您的網站不在 [youtube-dl 支持的網站列表](https://ytdl-org.github.io/youtube-dl/supportedsites.html)中時使用）不能強制使用一個特定的下載器。

如果您將 `--hls-prefer-native` 或 `--hls-prefer-ffmpeg` 放入您的配置中，則不同子集的影片將無法正確下載。相反，最好[提交一個問題](https://yt-dl.org/bug)或拉取請求，詳細說明為什麼原生或 ffmpeg HLS 下載器更適合您的用例。

### 您能添加對此動漫影片網站或免費播放當前電影的網站的支持嗎？

作為一項政策（以及合法性），youtube-dl 不包括對專門侵犯版權的服務的支持。根據經驗，如果您無法輕易找到該服務明顯被允許分發的影片（即由創作者、創作者的分銷商上傳，或以免費許可證發布），則該服務可能不適合包含在 youtube-dl 中。

服務上關於他們不託管侵權內容，而只是鏈接到那些託管侵權內容的聲明，證明該服務**不應**包含在 youtube-dl 中。如果服務的整個首頁都充滿了他們無權分發的影片，那麼任何 DMCA 通知也同樣沒有說服力。如果服務未經授權完整顯示受版權保護的影片，“合理使用”聲明也同樣沒有說服力。

但是，對確實購買了分發其內容權利的服務的支持請求是完全可以的。如有疑問，您可以簡單地包含提及合法購買內容的來源。

### 如何加快解決我的問題？

（也稱為：救命，我的重要問題沒有解決！）youtube-dl 核心開發團隊非常小。雖然我們盡力解決盡可能多的問題，但有時可能需要相當長的時間。要加快解決您的問題，您可以執行以下操作：

首先，請務必[在我們的問題跟踪器中報告問題](https://yt-dl.org/bugs)（https://yt-dl.org/bug 是此的別名）。這使我們能夠協調用戶和開發人員的所有努力，並作為一個統一的點。不幸的是，youtube-dl 項目已變得太大，無法將個人電子郵件用作有效的溝通渠道。

請閱讀下面的[錯誤報告說明](#錯誤)。許多錯誤都缺少所有必要的信息。如果可以，請向 youtube-dl 開發人員提供代理、VPN 或 shell 訪問權限。如果您能夠，請從多個國家/地區的多台計算機測試問題，以排除本地審查或配置錯誤問題。

如果沒有人有興趣解決您的問題，歡迎您親自解決並提交拉取請求（或強迫/付費他人這樣做）。

請隨時通過撰寫簡短評論（“問題在 youtube-dl 版本...中仍然存在，來自法國，但從比利時修復”）來不時地提升問題，但請不要每月超過一次。請不要將您的問題聲明為“重要”或“緊急”。

### 如何檢測給定 URL 是否受 youtube-dl 支持？

首先，請查看[支持的網站列表](docs/supportedsites.md)。請注意，有時網站可能會更改其 URL 方案（例如，從 https://example.com/video/1234567 到 https://example.com/v/1234567），並且 youtube-dl 報告該列表中某個服務的 URL 不受支持。在這種情況下，只需報告一個錯誤。

**無法**檢測 URL 是否受支持。這是因為 youtube-dl 包含一個通用提取器，它匹配**所有** URL。您可能會想禁用、排除或刪除通用提取器，但通用提取器不僅允許用戶從許多嵌入來自其他服務影片的網站中提取影片，還可以用於從託管自己的服務中提取影片。因此，我們既不建議也不支持禁用、排除或刪除通用提取器。

如果您想知道給定 URL 是否受支持，只需使用它調用 youtube-dl。如果您沒有收到任何影片，則該 URL 要麼不指向影片，要麼不受支持。您可以通過檢查輸出（如果您在控制台上運行 youtube-dl）或在從 Python 程序運行時捕獲 `UnsupportedError` 異常來找出原因。

# 為什麼我在提交錯誤時需要經過這麼多繁瑣的程序？

在我們有問題模板之前，儘管我們有詳細的[錯誤報告說明](#錯誤)，但我們收到的問題報告中約有 80% 是無用的，例如因為人們使用了數百個版本前的舊版本，因為簡單的語法錯誤（不是在 youtube-dl 中，而是在一般 shell 使用中），因為問題已經被多次報告過，因為人們沒有實際閱讀錯誤消息，即使它說“請安裝 ffmpeg”，因為人們沒有提及他們嘗試下載的 URL，以及許多其他簡單、易於避免的問題，其中許多與 youtube-dl 完全無關。

youtube-dl 是一個由太少志願者組成的開源項目，所以我們寧願花時間修復那些我們確定沒有這些簡單問題的錯誤，並且我們可以合理地自信地重現問題而無需反复詢問報告者。因此，`youtube-dl -v YOUR_URL_HERE` 的輸出是提交問題所需的全部內容。問題模板還會引導您完成一些可以執行的基本步驟，例如檢查您的 youtube-dl 版本是否為最新。

最後，請檢查您的問題，以避免下面列出的各種常見錯誤（您可以而且應該將此作為清單）。

### 問題本身的描述是否足夠？

我們經常收到難以理解的問題報告。為了避免後續的澄清，並幫助非英語母語的參與者，請詳細說明您正在請求什麼功能，或者您希望修復什麼錯誤。

確保顯而易見的是：

- 問題是什麼
- 如何修復
- 您提出的解決方案會是什麼樣子

如果您的報告少於兩行，則幾乎肯定缺少其中一些信息，這使得我們難以回應。我們通常太客氣而不會直接關閉問題，但缺少的信息很可能導致誤解。作為一名提交者，我經常對這些問題感到沮喪，因為我唯一可能推進它們的方法就是一遍又一遍地要求澄清。

對於錯誤報告，這意味著您的報告應包含使用 `-v` 標誌調用 youtube-dl 時的*完整*輸出。您收到的大多數錯誤消息甚至都這樣說，但您不會相信我們收到的錯誤報告中有多少沒有包含此信息。

如果您的服務器有多個 IP 或您懷疑存在審查，添加 `--call-home` 可能是一個好主意，以獲取更多診斷信息。如果錯誤是 `ERROR: Unable to extract ...` 並且您無法從多個國家/地區重現它，請添加 `--dump-pages`（警告：這將產生相當大的輸出，通過添加 `>log.txt 2>&1` 將其重定向到文件 `log.txt`）或將您在添加 `--write-pages` 時獲得的 `.dump` 文件上傳到[某處](https://gist.github.com/)。

**網站支持請求必須包含一個示例 URL**。示例 URL 是您可能想要下載的 URL，例如 `https://www.youtube.com/watch?v=BaW_jenozKc`。應該有一個明顯的影片存在。除非在非常特殊的情況下，影片服務的主頁（例如 `https://www.youtube.com/`）**不是**示例 URL。

### 問題是否已記錄？

確保沒有人已經打開您嘗試打開的問題。在窗口頂部搜索或瀏覽此儲存庫的 [GitHub Issues](https://github.com/ytdl-org/youtube-dl/search?type=Issues)。最初，至少使用搜索詞 `-label:duplicate` 以關注活動問題。如果存在問題，請隨意寫下類似“這也影響了我，版本為 2015.01.01。這是關於該問題的更多信息：...”的內容。雖然有些問題可能很舊，但對它們的新帖子通常會迅速激發活動。

### 您使用的是最新版本嗎？

在報告任何問題之前，請輸入 `youtube-dl -U`。這應該報告您已是最新版本。我們收到的報告中約有 20% 已經修復，但人們正在使用過時的版本。這也適用於功能請求。

### 為什麼現有選項不夠？

在請求新功能之前，請快速查看[支持選項列表](https://github.com/ytdl-org/youtube-dl/blob/master/README.md#options)。許多功能請求都是針對實際已經存在的功能！請務必在問題報告中展示您的工作，並詳細說明現有的類似選項如何**不**解決您的問題。

### 您的錯誤報告中是否有足夠的上下文？

人們希望解決問題，並且通常認為他們通過將更大的問題（例如，希望跳過已下載的文件）分解為特定請求（例如，請求我們在下載信息頁面之前查看文件是否存在）來幫助我們。然而，通常發生的情況是，他們將問題分解為兩個步驟：一個簡單的，一個不可能的（或極其複雜的）。

然後我們收到一個非常複雜的請求，而原始問題可以更容易地解決，例如通過將下載的影片 ID 記錄在單獨的文件中。為了避免這種情況，您必須在不明顯的情況下包含更大的上下文。特別是，每個不包括添加對新網站支持的功能請求都應包含一個用例場景，解釋在什麼情況下缺少的功能會有用。

### 問題是否只涉及一個問題？

我們的一些用戶似乎認為他們可以或應該打開的問題數量是有限的。他們可以或應該打開的問題數量沒有限制。雖然將所有問題轉儲到一個工單中可能看起來很有吸引力，但這意味著解決您其中一個問題的人無法將該問題標記為已關閉。通常，報告一堆問題會導致工單懸而未決，因為沒有人願意處理這個龐然大物，直到有人仁慈地將問題拆分為多個問題。

特別是，每個網站支持請求問題都應僅涉及一個網站的服務（通常在一個共同的域下，但始終使用相同的後端技術）。不要在同一個問題中請求對 vimeo 用戶影片、白宮播客和 Google Plus 頁面的支持。此外，請確保您不要將錯誤報告與功能請求一起發布。根據經驗，功能請求不包括與手頭功能沒有直接關係的 youtube-dl 輸出。不要將網絡錯誤報告與新影片服務的請求一起發布。

### 有人會需要這個功能嗎？

只發布您（或您可以親自交談的喪失能力的朋友）需要的功能。不要因為它們看起來是個好主意而發布功能。如果它們真的有用，它們將由需要它們的人請求。

### 您的問題是關於 youtube-dl 嗎？

這聽起來可能很奇怪，但我們收到的一些錯誤報告與 youtube-dl 完全無關，而是與不同的應用程序，甚至是報告者自己的應用程序有關。請確保您實際使用的是 youtube-dl。如果您正在使用 youtube-dl 的 UI，請向提供 UI 的實際應用程序的維護者報告錯誤。另一方面，如果您的 youtube-dl UI 以某種方式失敗，您認為與 youtube-dl 有關，那麼無論如何，請繼續報告錯誤。

# 版權

youtube-dl 由版權所有者發布到公共領域。

此 README 文件最初由 [Daniel Bolton](https://github.com/dbbolton) 編寫，同樣發布到公共領域。
