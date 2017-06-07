Emoji Alias
===

🌡

```
alias $'\355\240\274\355'='/opt/vc/bin/vcgencmd measure_temp'
```

> `\355\240\274\355` is the `Octal Escape Sequence` of `🌡`
> you can find it on http://graphemica.com/

⚙

```
alias $'\342\232\231'="sudo raspi-config"
```

🐧

```
alias $'\360\237\220\247'='uname -a'
```

🗑

```
alias $'\360\237\227\221'='rm -rf'
```

⬇

```
alias $'\342\254\207'='wget'
```

⏱

```
alias $'\342\217\261'='time'
```

💾

```
alias $'\360\237\222\276'='df -h'
```

📊

```
alias $'\360\237\223\212'='htop'
```

📴

```
alias $'\360\237\223\264'='sudo poweroff'
```

🐍

```
alias $'\360\237\220\215'='python'
```

🐳

```
alias $'\360\237\220\263'='docker'
```

🚬

```
alias $'\360\237\232\254'='free -m'
```

🐱

```
alias $'\360\237\220\261'='cat'
```

👓

```
alias $'\360\237\221\223'='whoami'
```

💻

```
alias $'\360\237\222\273'='hostname'
```

🚪

```
alias $'\360\237\232\252'='cd'
```

📋

```
alias $'\360\237\223\213'='cp'
```

📤

```
alias $'\360\237\223\244'='tar xf'
```

💣 ( do not use this one, this's just a joke )

```
#alias $'\360\237\222\243'='rm -rf /*'
```

and there is a bash script for get Emoji info:

```
#!/bin/bash
# run this scripts with `bash emoji-info.sh` or `./emoji-info.sh`

usage() {
  cat << EOF
usage: $0 [options] <emoji>

Options:
  -h        Show this message
  -o        Octal Escape Sequence
  -py       Python Source Code
  -n        Print name
  -u        Unicode Code Point
EOF
}

get_oct() {
  value=`curl -s "$url" | tr -d '\n'| awk -F '<td class='value'>|</td>' '{print $38}' | awk -F '>' '{print $2}'`
  echo "$value"
}

get_py() {
  value=`curl -s "$url" | tr -d '\n'| awk -F '<td class='value'>|</td>' '{print $44}' | awk -F '=' '{print $2}'| awk -F '>|<' '{print $2}'`
  echo "$value"
}

get_name() {
  value=`curl -s "$url" | tr -d '\n'| awk -F '<td>|</td>' '{print $368}'`
  echo "$value"
}

get_unicode() {
  value=`curl -s "$url" | tr -d '\n'| awk -F '<td class='value'>|</td>' '{print $2}' | awk -F '>' '{print $2}'`
  echo "$value"
}


if [ $# -eq 0 ]
then
  echo "Enter emoji and press [ENTER]: "
  read emoji
  url=graphemica.com/"$emoji"
  # echo "What info you want get:
  #       [-o] Octal Escape Sequence
  #      [-py] Python
  #       [-n] name        
  #       [-u] Unicode Code Point"
  usage
  echo "which info you want: "
  read opt

  case "$opt" in

       -o) get_oct "$url"
           exit
           ;;
      -py) get_py "$url"
           exit
           ;;
       -n) get_name "$url"
           exit
           ;;
       -u) get_unicode "$url"
           exit
           ;;
   esac

else

  emoji="$2"

  url=graphemica.com/"$emoji"

  case "$1" in

  -h|--help) usage
             exit
             ;;
         -o) get_oct "$url"
             exit
             ;;
        -py) get_py "$url"
             exit
             ;;
        -n) get_name "$url"
             exit
             ;;
        -u) get_unicode "$url"
             exit
             ;;
  esac

fi
```
