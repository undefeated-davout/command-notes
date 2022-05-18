# 共通

## システム環境設定

- PC名設定（共有 > コンピュータ名、編集ボタンからローカルホスト名 を変更）
- パーソナルファイアウォールON（セキュリティとプライバシー > ファイアウォール > ファイアウォールをオンにする）
- 暗号化（セキュリティとプライバシー > FileVault > FileVaultをオンにする）
- 画面ロック設定（[Macの画面を一瞬でロックする方法](https://book.mynavi.jp/macfan/detail_summary/id=38035)）
- スクロールを逆に（トラックパッド > スクロールとズーム > スクロールの方向 OFF）
- Dockを小さく
- マウスカーソル速度を最速に
- キーボードリピート入力時間を最短に
- キーバインドの変更（Caps Lockキーをcontrolキーに）
- 時計を２４時間表示、日付表示
（[私がMacを買ったらまず最初にする設定、インストールするアプリのまとめ](https://ushigyu.net/2016/03/09/mac-initial-configuration-apps/#US)）
- 単語登録

## インストール

- Chrome
- [英かな](https://ei-kana.appspot.com/)
- [Shiftit](https://github.com/fikovnik/ShiftIt/releases)
- [iTerm2](https://www.iterm2.com/)
- [Docker for Mac](https://hub.docker.com/editions/community/docker-ce-desktop-mac)
- [ATOM](https://atom.io/)
- [ATOM日本語化プラグイン](https://qiita.com/akikimur/items/bc342db92dbeb801ee61)
- [IntelliJ](https://www.jetbrains.com/idea/)
- [IntelliJ日本語化プラグイン](http://mergedoc.osdn.jp/#pleiades.html#PLUGIN)
- [Visual Studio Code](https://azure.microsoft.com/ja-jp/products/visual-studio-code/)
- [Sourcetree](https://ja.atlassian.com/software/sourcetree)
- [Workbench](https://www.mysql.com/jp/products/workbench/)
- [Clipy](https://clipy-app.com/)
- [Hidden Bar](https://apps.apple.com/jp/app/hidden-bar/id1452453066?mt=12)
- [AppCleaner](https://freemacsoft.net/appcleaner/)

## 設定

### プロファイル設定

~/.bash_profile

```bash
if [ -f ~/.bashrc ] ; then
. ~/.bashrc
fi

# zshをデフォルトにしないと警告出るのを非表示
export BASH_SILENCE_DEPRECATION_WARNING=1

# iTerm2
test -e "${HOME}/.iterm2_shell_integration.bash" && source "${HOME}/.iterm2_shell_integration.bash"
export PATH="/usr/local/opt/libxml2/bin:$PATH"

# anyenv
eval "$(anyenv init -)"
```

~/.bashrc

```bash
source /usr/local/Cellar/git/2.21.0/etc/bash_completion.d/git-prompt.sh
source /usr/local/Cellar/git/2.21.0/etc/bash_completion.d/git-completion.bash

# エイリアス
alias ll='exa -lahF --time-style=long-iso --no-permissions --no-user --icons'
alias lr='ll -s=modified -r'
alias cat='bat --paging=never'
alias catd='cat --decorations=never'

# 出力の後に改行を入れる
function add_line {
  if [[ -z "${PS1_NEWLINE_LOGIN}" ]]; then
    PS1_NEWLINE_LOGIN=true
  else
    printf '\n'
  fi
}
PROMPT_COMMAND='add_line'

GIT_PS1_SHOWDIRTYSTATE=true

export PS1='\[\033[34m\]\w\[\033[31m\]$(__git_ps1)\[\033[00m\]\$ '
```

※ ~/.bashrcでsourceで指定している部分は

```bash
find / -name git-prompt.sh
```

で検索した結果を記述する。

コマンド履歴の保存設定

```bash
echo 'shell_session_update' > $HOME/.bash_logout
```

### デフォルトシェルをbashに変更

```bash
chsh -s /usr/local/bin/bash
```

### Finderで隠しファイルを表示する設定

```bash
defaults write com.apple.finder AppleShowAllFiles TRUE
```

```bash
killall Finder
```

### XCode設定

```bash
vi /Applications/Xcode.app/Contents/Frameworks/IDEKit.framework/Versions/A/Resources/IDETextKeyBindingSet.plist
```

```bash
    <key>Edit</key>
    <dict>
        <key>Duplicate Line</key>
        <string>selectLine:, copy:, moveToBeginningOfLine:, paste:, moveToEndOfLine:</string>
    </dict>
```

```bash
Xcode > Preference > Key Bindings
Key Binding Set>Manage Key Bindings
+ボタンからDuplicate "Default"を選択しKey Binding Setを複製
```

### iTerm2設定

### ショートカット

Preferences > Keys > Hotkey を下記の通りにする。
（iTerm2を前面に表示させるショートカット）

```bash
Ctrl + i
```

### フルスクリーン設定

Preferences > General > Window > Native full screen windowsのチェックを外す

### .tmux.conf（マウススクロール有効設定）

```bash
# set-option -g mouse on
set-window-option -g mode-mouse on
set -g terminal-overrides 'xterm*:smcup@:rmcup@'
```

```bash
preferenceの
Profiles -> Terminal
Enable mouse reporting をON にする
```

## brewインストール

### Command Line Toolsインストール

```bash
xcode-select --install
```

### Homebrewインストール

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

### Gitインストール

```bash
brew install git
```

### プログラミングに最適なフォントの導入

```bash
brew tap sanemat/font
brew install ricty
cp -f /usr/local/Cellar/ricty/4.1.1/share/fonts/Ricty*.ttf ~/Library/Fonts/
fc-cache -vf
```

### よく使うbrew tools

```bash
# brew list -1

ansible
asciiquarium
bat
colordiff
exa
fzf
git
gotop
htop
jq
pyenv
skhd
sl
tmux
tree
yabai
z
```
