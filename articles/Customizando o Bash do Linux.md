# Customizando o Bash do Linux

```
if [ "$color_prompt" = yes ]; then
    hr='--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------'
    PS1='\n\[\e[0;34m\]$(printf "%s\n" "${hr:0:${COLUMNS:-$(tput cols)}}")\[\e[0;34m\]\n\[\e[0;35m\]«$(date +'%H:%M:%S')» \u → \e[0m\[\e[0;35m\]\e[0;31m$(__git_ps1 "[%s ✔]") \[\e[1;0m\]\n\[\e[0;34m\]\w/\[\e[1;0m\]\n\$ '
else
    PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
fi
unset color_prompt force_color_prompt
```