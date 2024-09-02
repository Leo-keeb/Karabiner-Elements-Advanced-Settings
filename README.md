# Karabiner-Elements-Advanced-Settings

このリポジトリにはKarabiner-ElementsのJSONファイルが４つ含まれています。現在私が設定しているファイルと３つのテンプレートファイルになります。以下は各ファイルの説明です。

## ファイル一覧

### 1. [MyAdvancedSetup_byLeo.json]
#### 概要:
このファイルは、現在私のMacbookで設定しているコードです。その他の３つのテンプレートファイルの機能を統合した複雑なものになります。
- **注意事項:** あらかじめ複数のキーをSimple Modificationsで変更しておく必要があるので、ただインポートしただけでは狙い通りに動かないかもしれません。

#### 具体的な機能:
準備中

---

### 2. [Template-HomeRowMods_byLeo.json]
#### 概要:
このファイルはHome Row Modsを実装するコードです。
ホームローにあるキー（a, s, d, f, j, k, l, -）を単独で押した場合には通常の文字を入力し、長押しした場合には修飾キー（Shift, Option, Control, Command）に変換します。これにより、通常のキー操作と修飾キーの操作を同時に簡単に行えるようにします。

#### 具体的な機能:
1. **`a`キー**:
   - 単独押し: 通常の`a`キーとして動作します。
   - 長押し: `Left Command`（左コマンド）キーとして動作します。
   - タイムアウトとしきい値は150msに設定されており、長押しが150ms以上続くとコマンドキーに変わります。

2. **`s`キー**:
   - 単独押し: 通常の`s`キーとして動作します。
   - 長押し: `Left Option`（左オプション）キーとして動作します。
   - 同様に、150msのタイムアウトとしきい値が設定されています。

3. **`d`キー**:
   - 単独押し: 通常の`d`キーとして動作します。
   - 長押し: `Left Control`（左コントロール）キーとして動作します。

4. **`f`キー**:
   - 単独押し: 通常の`f`キーとして動作します。
   - 長押し: `Left Shift`（左シフト）キーとして動作します。

5. **`j`キー**:
   - 単独押し: 通常の`j`キーとして動作します。
   - 長押し: `Right Shift`（右シフト）キーとして動作します。

6. **`k`キー**:
   - 単独押し: 通常の`k`キーとして動作します。
   - 長押し: `Right Control`（右コントロール）キーとして動作します。

7. **`l`キー**:
   - 単独押し: 通常の`l`キーとして動作します。
   - 長押し: `Right Option`（右オプション）キーとして動作します。

8. **`-`（ハイフン）キー**:
   - 単独押し: 通常の`-`キーとして動作します。
   - 長押し: `Right Command`（右コマンド）キーとして動作します。

#### パラメータ:
- `basic.to_if_alone_timeout_milliseconds` と `basic.to_if_held_down_threshold_milliseconds` は、150msに設定されており、この時間内にキーが離されないと長押しとみなされ、修飾キーとして動作します。
- `to_if_alone` は、キーが単独で押された場合に元の文字キーを入力する設定です。
- `to_if_held_down` は、キーが150ms以上長押しされた場合に修飾キーを発動させるための設定です。
- `to_delayed_action` は、キーが押されてすぐにキャンセルされた場合（意図しないキーの押し込みを防ぐため）に元の文字を入力するための設定です。

---

### 3. [Template-TapHold_byLeo.json]
#### 概要:
このコードはTapHold機能を実装するための設定です。具体的には、ボタンをタップ（短押し）した場合とホールド（長押し）した場合で異なるアクションを実行する機能を持っています。ホールドではレイヤーを切り替える機能が実装されます。
この設定は、`button16`と`button17`をベースに、タップ時に通常のバックスペースやEnterキーとして機能し、ホールド時にレイヤー切り替えを行う機能を提供します。また、条件付きで特定のキーが押されたときに他のキーコードにマッピングすることで、特定のレイヤーでの入力を実現しています（レイヤー機能）。さらに、**「・ー」のようにタップ後ホールドした場合、タップ時のコードが連続入力されます。**
- **注意事項:** あらかじめSimple Modificationsにて任意のキー２つを`button16`と`button17`に変更してください。(`button16`と`button17`以外の`button`でも構いませんが、`button1`や`button2`は通常クリックに割り当てられている点にご注意ください。)

#### 具体的な機能:
1. **`button16`のタップ**:
   - **タップ（短押し）**: `delete_or_backspace`キー（バックスペース）として動作します。タップ後ホールドした場合、`delete_or_backspace`キーが連続入力されます。

2. **`button17`のタップ**:
   - **タップ（短押し）**: `return_or_enter`キーとして動作します。タップ後ホールドした場合、`return_or_enter`キーが連続入力されます。

3. **レイヤー切り替えとリマップ**:
   - `button16`がホールドされている間（`temp_button16_hold_down`が`1`のとき）、`a`, `b`, `c`キーはそれぞれ`1`, `2`, `3`にリマップされます。`button17`は`8`にリマップされます。
   - `button17`がホールドされている間（`temp_button17_hold_down`が`1`のとき）、`a`, `b`, `c`キーはそれぞれ`4`, `5`, `6`にリマップされます。`button16`は`7`にリマップされます。


#### パラメータ:
- **`set_variable`**: 特定の変数を設定することで、キーの状態を管理し、条件付きアクションを実行します。これにより、ホールドされている間だけ特定のレイヤーが有効になります。
- **`conditions`**: 変数の状態に基づいて、特定のアクションが実行されるかどうかを決定します。これにより、特定のボタンがホールドされているときにのみ動作が変更されるようになります。
- **`to_delayed_action`**: ホールドがキャンセルされた場合や、指定された時間後に発動するアクションを設定します。

---

### 4. [Templates-Combo_byLeo.json]
#### 概要:
このコードは、特定のキーを同時に押すことで、入力モードを切り替える設定を実装しています。
この設定は、`X + C`キーの同時押しで英字入力（`Eisuu`）に切り替え、`,`と`.`キーの同時押しでかな入力（`Kana`）に切り替えるためのコンボキー機能を提供します。

#### 具体的な機能:
1. **`X + C`の同時押し**:
   - **コンボアクション**: `X`キーと`C`キーを同時に押すと、日本語入力モードから英字入力モード（`Eisuu`）に切り替わります。
   - **オプショナルモディファイア**: どのモディファイアキー（Shift, Controlなど）が押されていても、このコンボは機能します。

2. **`,`と`.`の同時押し**:
   - **コンボアクション**: `,`キーと`.`キーを同時に押すと、英字入力モードからかな入力モード（`Kana`）に切り替わります。
   - **オプショナルモディファイア**: このコンボも、モディファイアキーの影響を受けずに動作します。

#### パラメータ:
- **`simultaneous`**: 2つのキーを同時に押したときにアクションを発動するための設定です。この設定により、`X + C`や`,`と`.`などの特定のコンビネーションで特定のアクションがトリガーされます。
- **`modifiers.optional`**: モディファイアキーが押されている場合でも、コンボが機能するように設定されています。これにより、他のキーと組み合わせても動作が妨げられません。
