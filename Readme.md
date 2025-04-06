# git bash導入方法(20250406)
- 目的：vscodeの画面下部のターミナルでbashを使用
- 手順：
    1. vscode上で「ctrl+Shift+P」→「Preferences: Open User Settings (JSON)」を開く
    2. {}の中に以下を入力(profilesの中に他のものが合ってもよい)
    ```json
    "terminal.integrated.profiles.windows": {
        "GitBash": {
            "path": [
                "C:\\Git\\bin\\bash.exe"
            ],
            "args":["-l"],
            "icon": "terminal-bash"
        }
    },
    "terminal.integrated.defaultProfile.windows": "GitBash",
    ```
    3. デフォルトのターミナルを変更したい場合はvscode左上の「File」→「Preferences」→「Settings」→上部の検索窓で「terminal.integrated.defaultProfile.windows」を検索→タブの中から選択(もちろん手順3のdefaultProfileを直接変更してもよい)

# 仮想環境構築(20250406)
- 目的：壊れてもよい環境で作業したい，何をinstallする必要があるか明確にしたい
- 手順：
    1. 任意のバージョンのpythonを公式からglobalにインストール
    2. 以下のコマンドをターミナルに入力し環境構築
    ```bash
    # 任意のpythonバージョンx.xxの場合
    pythonx.xx -m venv [仮想環境名]
    #  pythonx.xxのコマンドがないといわれた場合
    py -x.xx -m venv [仮想環境名]
    ```
    3. 仮想環境をアクティベートし，pythonのバージョンが希望のものであれば成功
    ```bash
    source [仮想環境名]/Scripts/activate
    python --version
    ```
    4. 成功するとターミナルのカレントディレクトリ名の先頭に([仮想環境名])がでる．二行になる場合は以下のコマンドでファイル作成後に反映したら見やすくなる
    ```bash
    # nanoで.bashrcファイルを作成
    nano ~/.bashrc
    # 以下の書き込み終了後「ctrl+X」で保存して終了し環境に反映
    source ~/.bashrc

    # 書き込み内容は以下
    export VIRTUAL_ENV_DISABLE_PROMPT=1
    function set_venv_prompt {
    if [[ -n "$VIRTUAL_ENV" ]]; then
        venv_name="($(basename $VIRTUAL_ENV)) "
    else
        venv_name=""
    fi
    export PS1="${venv_name}\u@\h \W\$ "
    }
    PROMPT_COMMAND=set_venv_prompt
    ```
    - 今回は「C:\Users\ユーザー名/.bashrc」が作成された

# pyファイルの使用
- 目的：vscodeのコマンドでpyファイルを実行
- 手順：
    1. vscode上で「ctrl+Shift+P」→「Python: Select Interpreter」を開く
    2. 希望のpythonを選択

# ipynbファイルの使用
- 目的：仮想環境のpythonをipynbファイルでも使用
- 手順：
    1. 以下のコマンドでipykernelをインストール
    ```bash
    pip install ipykernel
    ```
    2. ipynbファイルの右上のカーネル選択から希望のものを選択
    3. 複数のipykernelを使い分けることも可能(未検証)
    ```bash
    python -m ipykernel install --user --name [仮想環境名] --display-name [カーネル名]
    ```z

