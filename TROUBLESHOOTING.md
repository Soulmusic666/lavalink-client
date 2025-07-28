# 🔧 Discord Music Bot - Troubleshooting Guide

## ❌ Common Errors & Solutions

### 1. **Error [TokenInvalid]: An invalid token was provided**

**Problem:** Bot cannot read Discord token from environment variables.

**Solutions:**

#### ✅ **Fix 1: Check .env file format**
```bash
# WRONG (with quotes):
DISCORD_TOKEN="MTxxxxxxxxxxxxxxxxxxxxx"

# CORRECT (without quotes):
DISCORD_TOKEN=MTxxxxxxxxxxxxxxxxxxxxx
```

#### ✅ **Fix 2: Ensure .env file exists**
```bash
cd testBot
cp .env.example .env
nano .env  # Edit with your actual token
```

#### ✅ **Fix 3: Check file permissions**
```bash
chmod 600 .env  # Secure permissions
ls -la .env     # Verify file exists
```

#### ✅ **Fix 4: Verify dotenv is installed**
```bash
npm list dotenv
# If not installed:
npm install dotenv
```

### 2. **Lavalink Connection Failed**

**Problem:** Bot cannot connect to Lavalink server.

**Solutions:**

#### ✅ **For Same VPS (Bot + Lavalink)**
```env
LAVALINK_HOST=localhost
# or
LAVALINK_HOST=127.0.0.1
```

#### ✅ **For Different Servers**
```env
LAVALINK_HOST=your_lavalink_server_ip
```

#### ✅ **Check Lavalink is Running**
```bash
# If using PM2:
pm2 list
pm2 logs lavalink

# If running manually:
java -jar Lavalink.jar
```

### 3. **No Audio Output**

**Problem:** Bot joins voice channel but no sound.

**Solutions:**

#### ✅ **Check Bot Permissions**
- Connect to voice channels
- Speak in voice channels
- Use voice activity

#### ✅ **Check Volume Settings**
```
!volume 75
```

#### ✅ **Try Different Audio Sources**
```
!play scsearch:never gonna give you up
!play ytsearch:bohemian rhapsody
```

### 4. **Search Not Working**

**Problem:** Bot cannot find music.

**Solutions:**

#### ✅ **Try Different Search Prefixes**
```
!play scsearch:song name    # SoundCloud (recommended)
!play ytsearch:song name    # YouTube
!play song name             # Auto-detect
```

#### ✅ **Check Lavalink Plugins**
Ensure your `application.yml` has proper plugin configuration.

### 5. **Bot Not Responding to Commands**

**Problem:** Bot online but doesn't respond to !commands.

**Solutions:**

#### ✅ **Check Message Content Intent**
Bot needs `MessageContent` intent enabled in Discord Developer Portal.

#### ✅ **Verify Command Prefix**
Commands must start with `!` (exclamation mark).

#### ✅ **Check Bot Permissions**
- Read Messages
- Send Messages
- Use Slash Commands (if applicable)

## 🔍 **Debug Mode**

For detailed troubleshooting, use debug version:

```bash
node debug-audio.js
```

This provides:
- ✅ Connection status logging
- ✅ Real-time playback monitoring
- ✅ Detailed error messages
- ✅ Audio stream information

## 📋 **Environment Checklist**

Before running the bot, ensure:

- [ ] ✅ Node.js v18+ installed
- [ ] ✅ npm dependencies installed (`npm install`)
- [ ] ✅ .env file created and configured
- [ ] ✅ Discord token added (without quotes)
- [ ] ✅ Lavalink server running and accessible
- [ ] ✅ Bot has proper Discord permissions
- [ ] ✅ Voice channel permissions configured

## 🆘 **Still Having Issues?**

1. **Check logs carefully** - error messages usually indicate the exact problem
2. **Test with debug-audio.js** - provides detailed diagnostic information
3. **Verify all environment variables** - ensure no typos or missing values
4. **Test connection separately** - use `test-connection.js` to isolate issues

## 📞 **Quick Test Commands**

```bash
# Test environment loading
node -e "require('dotenv').config(); console.log('Token loaded:', !!process.env.DISCORD_TOKEN);"

# Test basic connection
node test-connection.js

# Test with debug logging
node debug-audio.js

# Production bot
node music-player.js
```

---

**Most common issue: Quotes around token in .env file! Remove them! 🎯**