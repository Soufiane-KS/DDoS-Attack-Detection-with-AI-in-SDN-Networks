# DDoS Attack Detection with AI in SDN Networks

This project demonstrates a system that uses **Software Defined Networking (SDN)** and **Machine Learning (ML)** to detect and mitigate **Distributed Denial of Service (DDoS)** attacks in real time.

---

## 🔧 Technologies Used

- **Ryu SDN Controller** (Python-based)
- **Mininet** (for network emulation)
- **Scikit-learn** (for training the ML model)
- **Joblib** (for loading the saved model)
- **Python 3.x**

---

## 📊 ML Model

- Trained on a dataset with both benign and DDoS traffic.
- Uses the following features:
  - `pkt_rate`: Packet rate
  - `byte_rate`: Byte rate
  - `flag_syn`: TCP SYN flag
  - `flag_ack`: TCP ACK flag
- The model is a binary classifier (e.g., Decision Tree or Random Forest).
- Saved as `ddos_model.pkl` using `joblib`.

---

## ⚙️ How It Works

1. **Mininet** simulates a network with hosts and a switch.
2. The **Ryu controller** runs the `ddos_detector.py` app.
3. When a packet arrives:
   - Ryu extracts basic statistics (packet rate, byte rate, flags).
   - These are passed to the trained ML model.
   - If the model predicts **DDoS**, the packet is dropped.
   - Otherwise, it's forwarded normally.
4. Logs are printed in the terminal showing predictions in real time.

---

## 🧪 How to Run

### 1. Start Mininet

```
sudo mn --topo single,3 --mac --controller remote
```


2. Run the Ryu App
```
ryu-manager ryu_apps/ddos_detector.py
```

 ✅ Ensure ddos_model.pkl is in the correct directory (same as used in the Python file).

3. Send Test Traffic

You can simulate DDoS traffic using tools like hping3:
```
hping3 -S -p 80 --flood <target_ip>   # Simulates SYN flood (DDoS)
```


