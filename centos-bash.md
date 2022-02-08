# 以下を~/.bashrcへ記載

```bash
# git settings
source /usr/share/doc/git-1.8.3.1/contrib/completion/git-prompt.sh
source /usr/share/doc/git-1.8.3.1/contrib/completion/git-completion.bash
GIT_PS1_SHOWDIRTYSTATE=true
export PS1='\[\033[32m\]\u@\h\[\033[00m\]:\[\033[34m\]\w\[\033[31m\]$(__git_ps1)\[\033[00m\]\$ '

# for caution
# export PS1='\[\033[31m\]\u@\h\[\033[00m\]:\[\033[34m\]\w\[\033[31m\]$(__git_ps1)\[\033[00m\]\$ '
```

- for coutionは本番環境用に、サーバ情報部分を赤色にする設定
