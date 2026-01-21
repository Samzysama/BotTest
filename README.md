# Discord Event Scheduler Bot - Overview

This is a Discord bot for creating and managing event signups with role-based requirements, waitlists, and automated reminders.

## **Core Features:**
1. **Interactive Event Creation** - Users can create events via DM with custom roles/slots
2. **Reaction-based Signups** - Users click emojis to join events
3. **Role Requirements** - Can require specific Discord roles (e.g., "Avalonian Veteran" for Tank)
4. **Waitlist System** - Auto-manages waitlists when roles are full
5. **Event Management** - Edit times, cancel events, send reminders
6. **Persistent Storage** - Events saved to `events.json`
7. **Timezone Support** - Works with multiple timezones

## **Setup Instructions:**

### **1. Prerequisites**
```bash
python -m pip install discord.py pytz python-dateutil python-dotenv
```

### **2. Create Discord Application**
1. Go to [Discord Developer Portal](https://discord.com/developers/applications)
2. Create New Application → Bot
3. **Copy Bot Token** (keep this secret!)

### **3. Bot Permissions Required**
**General Permissions (Integer: 67488832):**
- View Channels
- Send Messages
- Manage Messages
- Embed Links
- Read Message History
- Add Reactions
- Use External Emojis

**Or use this OAuth2 URL with permissions:**
```
https://discord.com/api/oauth2/authorize?client_id=YOUR_CLIENT_ID&permissions=67488832&scope=bot
```

### **4. Environment Setup**
Create `.env` file:
```env
DISCORD_TOKEN=your_bot_token_here
```

### **5. Configuration Adjustments**
Edit these constants in the code:
```python
MOD_ROLE = "Raid Organizer"  # Role for event management
MAX_SLOTS = 50  # Maximum slots per role
ROLE_REQUIREMENTS = {  # Role restrictions
    "Tank": "Avalonian Veteran",
    "Healer": "Certified Healer"
}
DEFAULT_TZ = 'UTC'  # Default timezone
```

### **6. Required Discord Server Setup**
1. **Create the required roles:**
   - "Raid Organizer" (for moderators)
   - "Avalonian Veteran" (if using Tank requirements)
   - "Certified Healer" (if using Healer requirements)

2. **Ensure bot's role is positioned ABOVE** these roles in server settings

### **7. Run the Bot**
```bash
python BotSchedule.py
```

## **Key Commands:**
- `!create_event` - Start event creation via DM
- `!edit_event_time <message_id>` - Change event time (mod only)
- `!cancel_event <message_id>` - Cancel event (mod only)
- `!raider-help` - Get help in DMs
- `!ping` - Check bot latency
- `!restart` - Restart bot (owner only)

## **File Structure:**
```
BotSchedule.py          # Main bot code
events.json            # Auto-created event storage
bot.log               # Auto-created logs
.env                  # Your Discord token
```

## **Event Creation Format Example:**
When creating an event, use this format for roles:
```
🛡️ Tank:2
❤️ Healer:3
⚔️ DPS:10
```

**Time format:** `2023-12-25 20:00 EST`

## **Notes:**
1. Bot stores events in `events.json` - don't delete this file
2. Custom emojis must be from the same server
3. Bot requires **Manage Messages** permission to remove reactions
4. All participants get DMs for confirmations/reminders
5. Bot auto-restarts if crashes (with 10-second delay)

## **Troubleshooting:**
- **Bot doesn't respond**: Check token in `.env` is correct
- **Can't add reactions**: Bot needs "Add Reactions" permission
- **Role requirements not working**: Ensure bot role is above required roles
- **Events not saving**: Check file permissions for `events.json`

The bot will create `events.json` and `bot.log` automatically on first run.
