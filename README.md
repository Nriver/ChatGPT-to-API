# ChatGPT-to-API
Create a fake API using ChatGPT's website

> ## IMPORTANT
> You will not get free support for this repository. This was made for my own personal use and documentation will continue to be limited as I don't really need documentation. You will find more detailed documentation in the Chinese docs by a contributor.

**API endpoint: http://127.0.0.1:8080/v1/chat/completions.**

[中文文档（Chinese Docs）](https://github.com/xqdoo00o/ChatGPT-to-API/blob/master/README_ZH.md)
## Setup
    
### Authentication

Access token and PUID(only for PLUS account) retrieval has been automated by [OpenAIAuth](https://github.com/xqdoo00o/OpenAIAuth/) with account email & password.

`accounts.txt` - A list of accounts separated by new line 

Format:
```
email:password
...
```

All authenticated access tokens and PUID will store in `access_tokens.json`

Auto renew access tokens and PUID after 7 days

Caution! please use unblocked ip for authentication, first login to `https://chat.openai.com/` to check ip availability if you can.

### GPT-4 Model (Optional)

If you configured a PLUS account and use the GPT-4 model, a HAR file (`chat.openai.com.har`) is required to complete CAPTCHA verification

1. Use a chromium-based browser (Chrome, Edge) to login to `https://chat.openai.com/`, then open the browser developer tools (F12), and switch to the Network tab.

2. Create a new chat and select the GPT-4 model, ask a question at will, click the Export HAR button under the Network tab, export the file `chat.openai.com.har`

### API Authentication (Optional)

Custom API keys for this fake API, just like OpenAI api

`api_keys.txt` - A list of API keys separated by new line

Format:
```
sk-123456
88888888
...
```

## Getting set up
```  
git clone https://github.com/xqdoo00o/ChatGPT-to-API
cd ChatGPT-to-API
go build
./freechatgpt
```

### Environment variables
  - `SERVER_HOST` - Set to 127.0.0.1 by default
  - `SERVER_PORT` - Set to 8080 by default
  - `ENABLE_HISTORY` - Set to true by default

### Files (Optional)
  - `proxies.txt` - A list of proxies separated by new line

    ```
    http://127.0.0.1:8888
    ...
    ```
  - `access_tokens.json` - A JSON array of access tokens for cycling (Alternatively, send a PATCH request to the [correct endpoint](https://github.com/xqdoo00o/ChatGPT-to-API/blob/master/docs/admin.md))
    ```
    {"account1":{token:"access_token1", puid:"puid1"}, "account2":{token:"access_token2", puid:"puid2"}...}
    ```
  - `cookies.json` - A JSON that stores login cookies. If the OpenAI account is logged in with a third party such as Google, you can add a third-party account and any password in `accounts.txt`. Modify this file as follows to use it.
    ```
    {
        "third party username": [
            {
                "Name": "__Secure-next-auth.session-token",
                "Value": "After logging into a third-party account on browser，the value of __Secure-next-auth.session-token in cookies",
                "Path": "/",
                "Domain": "",
                "Expires": "0001-01-01T00:00:00Z",
                "MaxAge": 0,
                "Secure": true,
                "HttpOnly": true,
                "SameSite": 2,
                "Unparsed": null
            }
        ]
    }
    ```

## Admin API docs
https://github.com/xqdoo00o/ChatGPT-to-API/blob/master/docs/admin.md

## API usage docs
https://platform.openai.com/docs/api-reference/chat
