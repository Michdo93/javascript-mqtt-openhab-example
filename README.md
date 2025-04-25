# javascript-mqtt-openhab-example
A simple example of how to access an openHAB event bus via MQTT web socket in JavaScript using the example of a switch item, which is controlled via a button in HTML.

---

## 🌐 Live Demo
Open the `HTML` file in any modern web browser (make sure the MQTT broker is accessible over WebSocket).

---

## ⚙️ How It Works

This app:

1. Connects to an MQTT broker over WebSockets.
2. Subscribes to a specific topic to listen for state updates (`ON`/`OFF`).
3. Updates the button label based on the current switch state.
4. Allows the user to toggle the state via a button, which publishes a message to another MQTT topic.

---

## 📁 File Overview

- `mqtt.html`: The full working HTML file (no server needed, runs entirely in-browser).
- Uses [`mqtt.js`](https://github.com/mqttjs/MQTT.js) via CDN for WebSocket-based MQTT communication.

---

## 🔧 Customization Guide

### 🧭 Change MQTT Broker

Update this line in the HTML:

```js
const brokerUrl = 'ws://192.168.0.5:8083';
```

You can use:
- `ws://broker.hivemq.com:8000/mqtt` (public test broker)
- `wss://test.mosquitto.org:8081` (secure WebSocket)
- Your own broker with WebSocket support

---

### 🔐 Add Authentication (Username/Password)

Update the connection config like this:
```js
const client = mqtt.connect(brokerUrl, {
  clientId: 'mqtt_openhab_ui_' + Math.random().toString(16).substr(2, 8),
  username: 'yourUsername',
  password: 'yourPassword'
});
```

---

### 📡 Change Topics

#### Subscribe topic (state updates):
```js
const subscribeTopic = '/messages/states/iSmartHome_Hue_Lampen_Schalter';
```

#### Publish topic (to toggle device):
```js
const publishTopic = '/messages/commands/iSmartHome_Hue_Lampen_Schalter';
```

Just replace with your own MQTT topic names depending on your device setup.

---

### 💡 Customize Button Text

Update the `updateButtonLabel()` function:
```js
button.textContent = (state === 'ON') ? 'Switch OFF' : 'Switch ON';
```
You can change it to emojis, or local language if desired:
```js
button.textContent = (state === 'ON') ? '🔴 Turn Off' : '🟢 Turn On';
```

---

## 📋 Requirements

- A running MQTT broker with WebSocket support
- A web browser (Chrome, Firefox, Edge, etc.)
- Optional: MQTT device or simulator that listens to and publishes on the defined topics

---

## 🧪 Testing

You can use [MQTT Explorer](https://mqtt-explorer.com/) or command-line tools like `mosquitto_pub` and `mosquitto_sub` to test the topic manually.

---

## 🛡️ Security Note

This is a basic UI intended for local use or testing purposes. If you're using it in production:
- Always use `wss://` (secure WebSocket)
- Require authentication on the broker
- Do **not** expose unsecured brokers to the public internet

---

## 📜 License

MIT – free for personal or commercial use.

