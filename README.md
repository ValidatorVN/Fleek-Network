# Fleek-Network

Cấu hình khuyến cáo:

    Phase Devnet
    4 Core - 8 Gb ram - 150gb SSD.

Cài đặt và nâng cấp:

    sudo apt update && sudo apt upgrade -y
    
Cài đặt cần thiết để chạy node:

    sudo apt install git -y

    sudo apt-get install build-essential -y
    
    sudo apt-get install cmake clang pkg-config libssl-dev -y
    
    sudo apt-get install protobuf-compiler -y
    
    
Cài RUST: chọn số 1 nhấn Enter.

    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
    
    source "$HOME/.cargo/env"
    
Cài bổ sung cho cargo:

    cargo install sccache
   
1/ Tài về bộ cài đặt Node Fleek:

    git clone https://github.com/fleek-network/ursa.git
    cd ursa
    make install
    
 2/ Cài systemD cho tiện, dân chơi bây giờ ai xài tmux nữa:
 
    sudo tee /etc/systemd/system/ursa.service > /dev/null << EOF
    [Unit]
    Description=Ursa Node
    After=network-online.target
    [Service]
    User=$USER
    ExecStart=$(which ursa)
    Restart=on-failure
    RestartSec=10
    LimitNOFILE=10000
    [Install]
    WantedBy=multi-user.target
    EOF

Khởi chạy hệ thống, báo WARN như dưới đây là hoàn toàn bình thường:


    WARN: narwhal_primary::core: System shutting down
    at /root/.cargo/git/checkouts/sui-6ac459c53b1b685a/aa957af/narwhal/primary/src/core.rs:360
    in narwhal_primary::core::run_inner

Câu lệnh chạy node:

    sudo systemctl daemon-reload
    sudo systemctl enable ursa
    sudo systemctl restart ursa

Check logs:

    sudo journalctl -u ursa -f --no-hostname -o cat   
    
    
    Cộng đồng chạy Node & Validator VietNam, nơi thảo luận và chia sẻ kinh nghiệm về chạy node/validator.
    Chanel: https://t.me/RunnodeVietNamese
    Youtube: https://www.youtube.com/@nodevalidatorvietnam
    Twitter: https://twitter.com/NodeValidatorVN
    
    
