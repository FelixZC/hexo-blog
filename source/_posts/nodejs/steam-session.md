---
title: "Steam Session"
date: 2024-06-18
author: "pzc"
cover: /assets/images/jpg/16.jpg
categories: [Nodejs]
tags: [Steam]
---
`steam-session` 和 `steam-user` 是两个 Node.js 库，它们允许开发者与 Steam 社区和 Steam 服务进行交互。使用这两个库，你可以实现多种功能，包括但不限于：

- **登录和身份验证**：使用 `steam-user` 进行登录和身份验证，获取用户的身份信息。
- **好友列表**：获取和监控好友列表，包括好友的在线状态。
- **好友状态**：查看好友的在线状态，比如是否在线、离开、忙碌或隐身。
- **游戏状态**：查看好友当前正在玩的游戏。

以下是一些使用 `steam-user` 和 `steam-session` 可能实现的功能示例：

1. **登录和获取用户信息**：
   
   ```javascript
   const SteamUser = require('steam-user');
   
   const steamClient = new SteamUser();
   steamClient.logOn({
       accountName: 'your_steam_username',
       password: 'your_steam_password'
   });
   ```
   
2. **监听好友列表更新**：
   
   ```javascript
   steamClient.on('friendsList', (friends) => {
       friends.forEach((friend) => {
           console.log(`Friend ${friendpersonaName} is ${friend.status}`);
       });
   });
   ```
   
3. **检查好友是否在线**：
   
   ```javascript
   steamClient.on('friendPersonaState', (steamID, personaName, personaState) => {
       if (personaState === SteamUser.EPersonaState.Online) {
           console.log(`${personaName} is online.`);
       }
   });
   ```
   
4. **获取好友正在玩的游戏**：
   ```javascript
   steamClient.on('friendGamePlayed', (steamID, gameID, gameExtraInfo) => {
       console.log(`Friend is playing a game: ${gameExtraInfo}`);
   });
   ```
