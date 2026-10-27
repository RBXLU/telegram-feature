# Telegram Web A: Undo Send

Concept for @designers: hold an outgoing message for 5 seconds so it can be taken back.

## Behavior

- Settings → General → **Undo send** toggle (off by default).
- When enabled, a text or sticker message appears in the chat immediately with the clock icon, but is sent to the server only after 5 seconds.
- A toast "Sending message…" with a round timer and an **Undo** button is shown during the delay.
- Undo removes the local message and restores the text (and the reply quote) into the composer, unless the user has already started typing something new.
- Media, forwards, paid, scheduled messages and story replies are not delayed.
- Known limitation: closing the tab during the 5-second window drops the message.

The implementation reuses the client's existing pending local message flow (used by paid messages) and the timer toast pattern (used by paid reactions).

## Apply

```bash
git clone https://github.com/Ajaxy/telegram-tt.git
cd telegram-tt
git checkout 6002824b6532f3d913997ce496d9ab5f9b86bc22
git apply ../undo-send.patch
npm install
npm run dev
```

Open `http://localhost:1234/?test` to use the Telegram test server (phone numbers `99966XYYYY`, login code is the digit X repeated 5 times).

## Status

Not yet type-checked or run: `npm install` was blocked in the session where the patch was written.
