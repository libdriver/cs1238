[English](/README.md) | [ 简体中文](/README_zh-Hans.md) | [繁體中文](/README_zh-Hant.md) | [日本語](/README_ja.md) | [Deutsch](/README_de.md) | [한국어](/README_ko.md)

<div align=center>
<img src="/doc/image/logo.svg" width="400" height="150"/>
</div>

## LibDriver CS1238

[![MISRA](https://img.shields.io/badge/misra-compliant-brightgreen.svg)](/misra/README.md) [![API](https://img.shields.io/badge/api-reference-blue.svg)](https://www.libdriver.com/docs/cs1238/index.html) [![License](https://img.shields.io/badge/license-MIT-brightgreen.svg)](/LICENSE)

CS1238是一款高精度、低功耗Sigma-Delta模數轉換晶片，內寘一路Sigma-Delta ADC，兩路差分輸入通道和一路溫度感測器，ADC採用兩階sigma delta調製器，通過低雜訊儀用放大器結構實現PGA放大，放大倍數可選：1、2、64、128。 在PGA=128時，有效分辯率可達20.7比特（工作在5V）。CS1238內寘RC振盪器，無需外置晶振。 CS1238可以通過DRDY / DOUT和SCLK進行多種功能模式的配寘，例如用作溫度檢測、PGA選擇、ADC數據輸出速率選擇等等。 CS1238具有Power down模式。

LibDriver CS1238是LibDriver推出的CS1238全功能驅動，該驅動提供差分AD讀取功能並且它符合MISRA標準。

### 目錄

  - [說明](#說明)
  - [安裝](#安裝)
  - [使用](#使用)
    - [example basic](#example-basic)
  - [文檔](#文檔)
  - [貢獻](#貢獻)
  - [版權](#版權)
  - [聯繫我們](#聯繫我們)

### 說明

/src目錄包含了LibDriver CS1238的源文件。

/interface目錄包含了LibDriver CS1238與平台無關的GPIO模板。

/test目錄包含了LibDriver CS1238驅動測試程序，該程序可以簡單的測試芯片必要功能。

/example目錄包含了LibDriver CS1238編程範例。

/doc目錄包含了LibDriver CS1238離線文檔。

/datasheet目錄包含了CS1238數據手冊。

/project目錄包含了常用Linux與單片機開發板的工程樣例。所有工程均採用shell腳本作為調試方法，詳細內容可參考每個工程裡面的README.md。

/misra目錄包含了LibDriver MISRA程式碼掃描結果。

### 安裝

參考/interface目錄下與平台無關的GPIO模板，完成指定平台的GPIO驅動。

將/src目錄，您使用平臺的介面驅動和您開發的驅動加入工程，如果您想要使用默認的範例驅動，可以將/example目錄加入您的工程。

### 使用

您可以參考/example目錄下的程式設計範例完成適合您的驅動，如果您想要使用默認的程式設計範例，以下是它們的使用方法。

#### example basic

```C
#include "driver_cs1238_basic.h"

uint8_t res;
uint32_t i;
float ref = 3.3f;
int32_t temperature_raw = 0xC2000;
float temperature_deg = 23.0f;

/* init */
res = cs1238_basic_init(ref, temperature_raw, temperature_deg);
if (res != 0)
{
    return 1;
}

for (i = 0; i < 3; i++)
{
    double mv;

    /* delay 1000ms */
    cs1238_interface_delay_ms(1000);

    /* read data */
    res = cs1238_basic_read(&mv);
    if (res != 0)
    {
        cs1238_interface_debug_print("cs1238: read failed.\n");
        (void)cs1238_basic_deinit();

        return 1;
    }

    /* output */
    cs1238_interface_debug_print("cs1238: adc is %fmV.\n", mv);
}

/* deinit */
(void)cs1238_basic_deinit();

return 0;
```

### 文檔

在線文檔: [https://www.libdriver.com/docs/cs1238/index.html](https://www.libdriver.com/docs/cs1238/index.html)。

離線文檔: /doc/html/index.html。

### 貢獻

請參攷CONTRIBUTING.md。

### 版權

版權 (c) 2015 - 現在 LibDriver 版權所有

MIT 許可證（MIT）

特此免費授予任何獲得本軟件副本和相關文檔文件（下稱“軟件”）的人不受限制地處置該軟件的權利，包括不受限制地使用、複製、修改、合併、發布、分發、轉授許可和/或出售該軟件副本，以及再授權被配發了本軟件的人如上的權利，須在下列條件下：

上述版權聲明和本許可聲明應包含在該軟件的所有副本或實質成分中。

本軟件是“如此”提供的，沒有任何形式的明示或暗示的保證，包括但不限於對適銷性、特定用途的適用性和不侵權的保證。在任何情況下，作者或版權持有人都不對任何索賠、損害或其他責任負責，無論這些追責來自合同、侵權或其它行為中，還是產生於、源於或有關於本軟件以及本軟件的使用或其它處置。

### 聯繫我們

請聯繫lishifenging@outlook.com。