# My Espanso code

## Basic command 

First, copy a valid IP address, then type `:ip`.
Espanso runs the Linux command in the background and then it outputs the result anywhere. Also, it is copied to your clipboard.

<img src="doc/linux.gif" width="900">

<details>

<summary>Sample Code</summary>

```
  - trigger: ":ip"
    replace: "{{output}}"
    label: "ip"
    vars:
      - name: output
        type: shell
        params:
          cmd: '/usr/bin/curl "ipinfo.io/$(pbpaste)" && whois -h bgp.tools $(pbpaste)'
      - name: clipboard_contents
        type: clipboard

```
</details>

</details>


## Type a dynamic variable

When you type `:curl`, you will see options to select either the Performance option, resolver option or a POST request.
After selecting one, you can enter the domain to access. The generated cURL command is then displayed directly at the cursor.

<img src="doc/curl.gif" width="900">

<details>

<summary>Sample Code</summary>

```
matches:
  - trigger: ":curl"
    replace: "curl -svo /dev/nul -w 'http_code:%{http_code}\\ntime_namelookup:%{time_namelookup}\\ntime_connect:%{time_connect}\\ntime_appconnect:%{time_appconnect}\\ntime_pretransfer:%{time_pretransfer}\\ntime_starttransfer:%{time_starttransfer}\\ntime_total:%{time_total}\\n' https://{{form1.name}}"
    label: "curl performance"
    vars:
    - name: form1
      type: form
      params:
        layout: |
          Type in Domain [[name]]

  - trigger: ":curl"
    replace: "curl -svo /dev/nul -w 'http_code:%{http_code}\\ntime_namelookup:%{time_namelookup}\\ntime_connect:%{time_connect}\\ntime_appconnect:%{time_appconnect}\\ntime_pretransfer:%{time_pretransfer}\\ntime_starttransfer:%{time_starttransfer}\\ntime_total:%{time_total}\\n' https://{{form1.name}} --resolve '{{form1.name}}:443:{{form1.ip}}'"
    label: "curl performance with resolve"
    vars:
    - name: form1
      type: form
      params:
        layout: "Type in Domain [[name]] \nType in IP [[ip]]"

  - trigger: ":curl"
    replace: "curl -svo /dev/nul https://{{form1.name}} -d '{{form1.post}}' -X POST"
    label: "curl performance with POST"
    vars:
    - name: form1
      type: form
      params:
        layout: "Type in Domain [[name]] \nType in Data [[post]]"
```
</details>

</details>

### POP Search

By typing `:pop` anywhere, you can easily check Fastly's POP name, country, and region. Its geolocation data is automatically copied to your clipboard, allowing you to check the location on Google Maps. This eliminates the need to remember a large number of POP names and locations.

https://www.fastly.com/documentation/guides/concepts/pop/

<img src="doc/pop_search.gif" width="900">

<details>

<summary>Sample Code</summary>

```
  - trigger: ":pop"
    replace: "{{output}}"
    label: "POP: ADL | City: Adelaide | Country: Australia"
    vars:
      - name: output
        type: shell
        params:
          cmd: 'echo "https://www.google.com/maps/search/?api=1&query=-34.9285,138.6007" | pbcopy'

  - trigger: ":pop"
    replace: "{{output}}"
    label: "POP: AMS | City: Amsterdam | Country: Netherlands"
    vars:
      - name: output
        type: shell
        params:
          cmd: 'echo "https://www.google.com/maps/search/?api=1&query=52.308613,4.763889" | pbcopy'
```

</details>

### Setup 

1. Install using Homebrew
See below for details.
https://espanso.org/docs/install/mac/

2. Git clone
```
git clone https://github.com/fastly/espanso-conf.git
```

3. Copy this github Config to your folder

```
cp -R ./espanso-conf/espanso/match/* $HOME/Library/Application\ Support/espanso/match/
```
See below for details.
https://espanso.org/docs/configuration/basics/#structure 
