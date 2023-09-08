# nesorter-discord
## Discord bot for playing music from web-radio

### How to use

- Init Node.JS package/project
```bash
mkdir radio-restream && \
cd radio-restream && \
npm init -f
```

- Next, install this lib
```bash
npm install @nesorter/discord-stream-lib@latest
```

- Next, create `index.js` and paste this code:
```js
const { Bot } = require('@nesorter/discord-stream-lib');

Bot({
  // bot token, yeah
  BOT_TOKEN: 'secret', 

  // custom name for bot
  BOT_SELF_RENAME_TO_NAME: 'restream', 

  // id of voice chat where bot streams music
  VOICE_CHAT_ID: '529772279727652864', 

  // url to your web-radio
  STREAM_MOUNTPOINT: 'http://kugi.club:3002/listen',

  // custom idv3 tags injecting to discord bot profile
  onTrackMetadataRequested: async () => {
    // here you can call external api, ex:
    // const data = await axios('http://radio.com/api/current');

    return {
      artist: 'Artist 2',
      title: 'Title 2',
    };
  },
}).then(({ client, audioPlayer, audioResource }) => {
  // this callback will be called when init done
  // here you can control bot and audio by yourself (if you need), so:

  // client - https://old.discordjs.dev/#/docs/discord.js/main/class/Client
  // audioPlayer - https://discord.js.org/docs/packages/voice/main/AudioPlayer:Class
  // audioResource - https://discord.js.org/docs/packages/voice/main/AudioResource:Class
});
```
