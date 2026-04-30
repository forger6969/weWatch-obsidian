---
type: client
tags: [weWatch, mobile, react-native]
---
# 📱 Mobile App

**Tech:** React Native + Expo | **Owner:** [[../people/Emirhan]]
**Hub:** [[../00-weWatch-Overview]]

## Стек
- React Native + TypeScript
- Expo Go (dev) / EAS Build (prod)
- [[../concepts/FCM]] — push notifications
- [[../concepts/Socket.io]] — WatchParty sync

## Главные экраны
- Auth: Register → Verify → Login → ProfileSetup
- Home: Trending, Top-rated, Rooms
- WatchParty: Player, Chat, Members
- Battle: Create, Active, Results
- Profile: Stats, Friends, Achievements

## Связи
- → [[auth]] — OAuth flows
- → [[content]] — поиск и видео
- → [[watch-party]] — Socket.io
- → [[battle]] — gamification
- → [[notification]] — FCM tokens
