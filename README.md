# Codelab
[Intro to state in Compose](https://developer.android.com/codelabs/basic-android-kotlin-compose-using-state?hl=ja&continue=https://developer.android.com/courses/pathways/android-basics-compose-unit-2-pathway-3?hl%3Dja%23codelab-https://developer.android.com/codelabs/basic-android-kotlin-compose-using-state#11)

# Practice Branch
- starter
- state
- main

# Summary about Tests
- 自動テストの概要
- 自動テストが重要である理由
- ローカルテストとインストルメンテーション テストの違い
- 自動テストの作成に関する基本的なベスト プラクティス
- Android プロジェクト内でローカルテストとインストルメンテーション テストのクラスが配置される場所と配置すべき場所
- テストメソッドを作成する方法
- ローカルテストとインストルメンテーション テストのクラスを作成する方法
- ローカルテストとインストルメンテーション テストでアサーションを作成する方法
- テストルールを使用する方法
- ComposeTestRule を使用してテストでアプリを起動する方法
- インストルメンテーション テストでコンポーザブルを操作する方法
- テストを実行する方法

# Memo about Tests
- 単体テストはメソッド単位のテスト、インストルメンテーションテストはUIのテスト
- private -> internalにするが、@VisibleForTestingでテスト目的でパブリックにしていることを明示する
- アプリコードが main > java > com > example > tiptime パッケージに作成されている場合、ローカルテストは test > java
- instrumentation testはandroidTest、local(unit) testはtest[unitTest]
- assetsは色々ある（assertEquals()、assertNotEquals()、assertTrue()、assertFalse()、assertNull()、assertNotNull()、assertThat()）
- composeはonNodeWithTextでノードにアクセスできる
- 詳細は別のCodeLabでやるが、テストを書く癖をつけよう

# Example
- Unit Test
  ```
  class TipCalculatorTests {

    @Test
    fun calculateTip_20PercentNoRoundup() {
        val amount = 10.00
        val tipPercent = 20.00
        val expectedTip = NumberFormat.getCurrencyInstance().format(2)
        val actualTip = calculateTip(
            amount = amount,
            tipPercent = tipPercent,
            roundUp = false
        )

        assertEquals(expectedTip, actualTip)
    }
  }
- Instrumentation Test
  ```
  class TipUITests {
  
      @get:Rule
      val composeTestRule = createComposeRule()
  
      @Test
      fun calculate_20_percent_tip() {
          composeTestRule.setContent {
              TipTimeTheme {
                  TipTimeLayout()
              }
          }
          composeTestRule.onNodeWithText("Bill Amount").performTextInput("10")
          composeTestRule.onNodeWithText("Tip Percentage").performTextInput("20")
          val expectedTip = NumberFormat.getCurrencyInstance().format(2)
          
          composeTestRule.onNodeWithText("Tip Amount: $expectedTip").assertExists(
              "No node with this text was found."
          )
      }
  }
  ```
# Official README

Tip Time - Solution Code
=================================

Solution code for the [Android Basics with Compose](https://developer.android.com/courses/android-basics-compose/course): Tip Time app.


Introduction
------------
The Tip Time app contains various UI elements for calculating a tip,
teaching about user input, and State in Compose.


Pre-requisites
--------------
* Experience with Kotlin syntax.
* How to create and run a project in Android Studio.


Getting Started
---------------
1. Install Android Studio, if you don't already have it.
2. Download the sample.
3. Import the sample into Android Studio.
4. Build and run the sample.
