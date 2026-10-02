[English](/README.md) | [ 简体中文](/README_zh-Hans.md) | [繁體中文](/README_zh-Hant.md) | [日本語](/README_ja.md) | [Deutsch](/README_de.md) | [한국어](/README_ko.md)

<div align=center>
<img src="/doc/image/logo.svg" width="400" height="150"/>
</div>

## LibDriver CS1238

[![MISRA](https://img.shields.io/badge/misra-compliant-brightgreen.svg)](/misra/README.md) [![API](https://img.shields.io/badge/api-reference-blue.svg)](https://www.libdriver.com/docs/cs1238/index.html) [![License](https://img.shields.io/badge/license-MIT-brightgreen.svg)](/LICENSE)

CS1238は、1つのシグマ・デルタADC、2つの差動入力チャンネル、および1つの温度センサを内蔵した、高精度かつ低消費電力のシグマ・デルタ方式A/Dコンバータ・チップです。このADCは2段構成のシグマ・デルタ変調器を採用し、低ノイズの計装アンプ構造によってPGA（プログラマブル・ゲイン・アンプ）増幅を実現しています。増幅率は1、2、64、128から選択可能です。PGA設定が128の場合、有効分解能は20.7ビットに達します（5V動作時）。CS1238はRC発振器を内蔵しており、外付けの水晶発振器を必要としません。DRDY/DOUTおよびSCLK端子を介して、温度検出、PGA設定、ADCデータ出力レートの選択など、複数の動作モードを設定できます。また、CS1238にはパワーダウン・モードも搭載されています。

LibDriver CS1238は、LibDiverによって起動されたCS1238の全機能ドライバーであり、差分広告読み取り機能を提供します。LibDriverはMISRAに準拠しています。

### 目次

  - [説明](#説明)
  - [インストール](#インストール)
  - [使用](#使用)
    - [example basic](#example-basic)
  - [ドキュメント](#ドキュメント)
  - [貢献](#貢献)
  - [著作権](#著作権)
  - [連絡して](#連絡して)

### 説明

/ srcディレクトリには、LibDriver CS1238のソースファイルが含まれています。

/ interfaceディレクトリには、LibDriver CS1238用のプラットフォームに依存しないGPIOバステンプレートが含まれています。

/ testディレクトリには、チップの必要な機能を簡単にテストできるLibDriver CS1238ドライバーテストプログラムが含まれています。

/ exampleディレクトリには、LibDriver CS1238プログラミング例が含まれています。

/ docディレクトリには、LibDriver CS1238オフラインドキュメントが含まれています。

/ datasheetディレクトリには、CS1238データシートが含まれています。

/ projectディレクトリには、一般的に使用されるLinuxおよびマイクロコントローラー開発ボードのプロジェクトサンプルが含まれています。 すべてのプロジェクトは、デバッグ方法としてシェルスクリプトを使用しています。詳細については、各プロジェクトのREADME.mdを参照してください。

/ misraはLibDriver misraコードスキャン結果を含む。

### インストール

/ interfaceディレクトリにあるプラットフォームに依存しないGPIOバステンプレートを参照して、指定したプラットフォームのGPIOバスドライバを完成させます。

/src ディレクトリ、プラットフォームのインターフェイス ドライバー、および独自のドライバーをプロジェクトに追加します。デフォルトのサンプル ドライバーを使用する場合は、/example ディレクトリをプロジェクトに追加します。

### 使用

/example ディレクトリ内のサンプルを参照して、独自のドライバーを完成させることができます。 デフォルトのプログラミング例を使用したい場合の使用方法は次のとおりです。

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

### ドキュメント

オンラインドキュメント: [https://www.libdriver.com/docs/cs1238/index.html](https://www.libdriver.com/docs/cs1238/index.html)。

オフラインドキュメント: /doc/html/index.html。

### 貢献

CONTRIBUTING.mdを参照してください。

### 著作権

著作権（c）2015-今 LibDriver 全著作権所有

MITライセンス（MIT）

このソフトウェアおよび関連するドキュメントファイル（「ソフトウェア」）のコピーを取得した人は、無制限の使用、複製、変更、組み込み、公開、配布、サブライセンスを含む、ソフトウェアを処分する権利を制限なく付与されます。ソフトウェアのライセンスおよび/またはコピーの販売、および上記のようにソフトウェアが配布された人の権利のサブライセンスは、次の条件に従うものとします。

上記の著作権表示およびこの許可通知は、このソフトウェアのすべてのコピーまたは実体に含まれるものとします。

このソフトウェアは「現状有姿」で提供され、商品性、特定目的への適合性、および非侵害の保証を含むがこれらに限定されない、明示または黙示を問わず、いかなる種類の保証もありません。 いかなる場合も、作者または著作権所有者は、契約、不法行為、またはその他の方法で、本ソフトウェアおよび本ソフトウェアの使用またはその他の廃棄に起因または関連して、請求、損害、またはその他の責任を負わないものとします。

### 連絡して

お問い合わせくださいlishifenging@outlook.com。