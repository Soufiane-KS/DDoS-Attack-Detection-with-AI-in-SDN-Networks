# DDoS-Attack-Detection-with-AI-in-SDN-Networks

DDoS Attack Detection with AI in SDN Networks

This project demonstrates a system that uses Software Defined Networking (SDN) and Machine Learning (ML) to detect and mitigate Distributed Denial of Service (DDoS) attacks in real time.
🔧 Technologies Used

    Ryu SDN Controller (Python-based)

    Mininet (for network emulation)

    Scikit-learn (for training the ML model)

    Joblib (for loading the saved model)

    Python 3.x

📁 Project Structure

project/
│
├── ryu_apps/
│   └── ddos_detector.py       # Ryu app with ML-based detection
├── models/
│   └── ddos_model.pkl         # Trained machine learning model
├── traffic_gen/
│   └── simulate_ddos.py       # Script to generate normal/DDoS traffic (optional)
└── README.md

📊 ML Model

    Trained on a dataset with both benign and DDoS traffic.

    Uses features such as:

        pkt_rate: Packet rate

        byte_rate: Byte rate

        flag_syn: TCP SYN flag

        flag_ack: TCP ACK flag

    The model is a binary classifier (e.g., Decision Tree or Random Forest).

    Saved as ddos_model.pkl using joblib.

⚙️ How It Works

    Mininet simulates a network with hosts and a switch.

    The Ryu controller runs the ddos_detector.py app.

    When a packet arrives:

        Ryu extracts basic statistics (packet rate, byte rate, flags).

        These are passed to the trained ML model.

        If the model predicts DDoS, the packet is dropped.

        Otherwise, it's forwarded normally.

    Logs are printed in the terminal showing predictions in real time.

🧪 How to Run
1. Start Mininet

sudo mn --topo single,3 --mac --controller remote

2. Run the Ryu App

ryu-manager ryu_apps/ddos_detector.py

Make sure ddos_model.pkl is in the correct location.
3. Send Test Traffic

You can test detection using ping, iperf, or a custom traffic generator:

hping3 -S -p 80 --flood <target_ip>   # Simulates SYN flood (DDoS)

🛡️ Output Example

Features for 10.0.0.1 -> 10.0.0.3: {'pkt_rate': 100, 'byte_rate': 10000, 'flag_syn': 1, 'flag_ack': 0}
Prediction for 10.0.0.1: DDoS
DDoS detected from 10.0.0.1. Packet dropped.

📈 Future Improvements

    Use more advanced features (e.g., flow duration, packet intervals)

    Add real-time traffic visualization dashboard

    Integrate with a database for logging attack details
