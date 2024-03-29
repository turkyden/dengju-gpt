<h1 align="center">Dengju GPT</h1>

<p align="center">A ChatGPT APP < 100 lines of code</p>

![Slide 16_9 - 1 (1)](https://user-images.githubusercontent.com/24560160/223464736-7c3dddd6-028e-49ad-9150-0a3ac5e7fe35.png)

## Source

```html
<!DOCTYPE html>
<html>
  <head>
    <title>100 行代码手写 chatgpt</title>
    <meta charset="UTF-8" />
    <script src="https://cdn.jsdelivr.net/npm/vue@2"></script>
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no,viewport-fit=cover"
    />
  </head>
  <body>
    <a id="github-link" href="https://github.com/turkyden/dengju-gpt" title="Follow me on GitHub" aria-label="Follow me on GitHub" rel="noopener" target="_blank" style="position: absolute; top: 0px; right: 0px; color: white;"><svg width="80" height="80" viewBox="0 0 250 250" aria-hidden="true"><path d="M0,0 L115,115 L130,115 L142,142 L250,250 L250,0 Z"></path><path d="M128.3,109.0 C113.8,99.7 119.0,89.6 119.0,89.6 C122.0,82.7 120.5,78.6 120.5,78.6 C119.2,72.0 123.4,76.3 123.4,76.3 C127.3,80.9 125.5,87.3 125.5,87.3 C122.9,97.6 130.6,101.9 134.4,103.2" fill="currentColor" class="octo-arm" style="transform-origin: 130px 106px;"></path><path d="M115.0,115.0 C114.9,115.1 118.7,116.5 119.8,115.4 L133.7,101.6 C136.9,99.2 139.9,98.4 142.2,98.6 C133.8,88.0 127.5,74.4 143.8,58.0 C148.5,53.4 154.0,51.2 159.7,51.0 C160.3,49.4 163.2,43.6 171.4,40.1 C171.4,40.1 176.1,42.5 178.8,56.2 C183.1,58.6 187.2,61.8 190.9,65.4 C194.5,69.0 197.7,73.2 200.1,77.6 C213.8,80.2 216.3,84.9 216.3,84.9 C212.7,93.1 206.9,96.0 205.4,96.6 C205.1,102.4 203.0,107.8 198.3,112.5 C181.9,128.9 168.3,122.5 157.7,114.1 C157.9,116.9 156.7,120.9 152.7,124.9 L141.0,136.5 C139.8,137.7 141.6,141.9 141.8,141.8 Z" fill="currentColor"></path></svg></a>
    <div id="app" style="padding: 4rem 0">
      <h1 style="text-align: center;">Dengju GPT 🤖</h1>
      <p style="text-align: center;">@dengjudeng</p>

      <br />

      <div style="text-align: center;">
        <input
          :disabled="isTyping"
          v-model="message"
          style="width: calc(100% - 4rem); padding: 0.5rem;"
          autofocus
          :placeholder="isTyping ? 'ChatGPT 正在组织语言 ...' : '问问 ChatGPT ...'"
          type="text"
          @blur="handleSend"
          @keyup.enter="handleSend"
        />
      </div>

      <br />

      <ul v-for="(message, key) in [...messages].reverse()" :key="key">
        <li>
          <div style="color: #6b7280;">{{ message.role }}</div>
          <div style="white-space: pre-wrap;">{{message.content}}</div>
        </li>
      </ul>
    </div>
    <script>
      new Vue({
        el: "#app",
        data() {
          return {
            message: "",
            isTyping: false,
            messages: [
              {
                content: "Hi, 我是 ChatGPT！你可以问我任何事情！👋",
                role: "assistant"
              }
            ]
          };
        },
        methods: {
          handleSend: async function () {
            if(!this.message) return
            const newMessage = {
              content: this.message,
              role: "user"
            };
            const newMessages = [...this.messages, newMessage];
            this.messages = newMessages;
            this.isTyping = true;
            await this.processMessageToChatGPT(newMessages);
            this.isTyping = false;
          },
          processMessageToChatGPT: async function (messages) {
            const API_KEY = "sk-XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX";
            const apiRequestBody = {
              model: "gpt-3.5-turbo",
              messages: messages
            };
            this.message = "";
            const data = await fetch(
              "https://api.openai.com/v1/chat/completions",
              {
                method: "POST",
                headers: {
                  Authorization: "Bearer " + API_KEY,
                  "Content-Type": "application/json"
                },
                body: JSON.stringify(apiRequestBody)
              }
            ).then((data) => data.json());
            this.messages = [
              ...messages,
              {
                content: data.choices[0].message.content,
                role: "assistant"
              },
            ];
          }
        }
      });
    </script>
  </body>
</html>
```

## ✨ 关注我

这是作者的微信「视频号」，每天分享一些有趣的 SaaS 小软件，欢迎关注 ~

<img width="200" src="https://user-images.githubusercontent.com/24560160/230781326-de84d919-1410-4b8a-ad81-3b0f6ffbe7d2.png">
