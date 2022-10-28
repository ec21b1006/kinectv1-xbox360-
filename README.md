# Kinect V1(XBOX360)

## Using without ROS

1. As always, start with an update and upgrade

    ```sudo apt-get update```

    ```sudo apt-get upgrade```

2. Install the dependencies
    
    ```sudo apt-get install git-core cmake freeglut3-dev pkg-config build-essential libxmu-dev libxi-dev libusb-1.0-0-dev```

3. Get the libfreenect repository from GitHub

    ```git clone https://github.com/OpenKinect/libfreenect.git```

4. Make and install
    ```
    cd libfreenect
    mkdir build 
    cd build
    cmake -L ..
    sudo make install
    sudo ldconfig /usr/local/lib64/
    ```
5. To use kinect without sudoing every time

    ```
    sudo adduser $USER video
    sudo adduser $USER plugdev
    ```
6. Next we will add some device rules
    ```
    sudo nano /etc/udev/rules.d/51-kinect.rules
    ```
7. Paste the following and ctrl+q to save
    ```
    # ATTR{product}=="Xbox NUI Motor"
    SUBSYSTEM=="usb", ATTR{idVendor}=="045e", ATTR{idProduct}=="02b0", MODE="0666"
    # ATTR{product}=="Xbox NUI Audio"
    SUBSYSTEM=="usb", ATTR{idVendor}=="045e", ATTR{idProduct}=="02ad", MODE="0666"
    # ATTR{product}=="Xbox NUI Camera"
    SUBSYSTEM=="usb", ATTR{idVendor}=="045e", ATTR{idProduct}=="02ae", MODE="0666"
    # ATTR{product}=="Xbox NUI Motor"
    SUBSYSTEM=="usb", ATTR{idVendor}=="045e", ATTR{idProduct}=="02c2", MODE="0666"
    # ATTR{product}=="Xbox NUI Motor"
    SUBSYSTEM=="usb", ATTR{idVendor}=="045e", ATTR{idProduct}=="02be", MODE="0666"
    # ATTR{product}=="Xbox NUI Motor"
    SUBSYSTEM=="usb", ATTR{idVendor}=="045e", ATTR{idProduct}=="02bf", MODE="0666"
    ```
8. Go back in the directory to */libfreenect*. Now we need to generate audio drivers for support, run the following to get ‘audios.bin’ file. To get this file we need run the python script given below
    ```
    python3 src/fwfetcher.py
    ```
9. Now we need to copy ‘audios.bin’ to a specific location
    ```
    sudo cp audios.bin /usr/local/share/libfreenect/
    ```
10. Run the following to check the audio
    ```
    freenect-micview
    ```
    You should see this
    ![image](https://lh3.googleusercontent.com/o2D7snHQYGEzOK0hFATuB5xAXwyRfYl5hx9EXhLJvRNH7l642vm4RLCfT27_bsA0tGMEBSmnovuG0Ydg73qZDjt4bom1spNjwuatagOrmnfF0uVbncc3bX8eQqXiRgTiWjQ5FWKcryUHY4zHR1r75RCEO_j5RF7SEB2kAxfyDXCtecaKZ1Sbk6OT-ULfb1SJ9V8G0XhgFHdZK6fsfMsinG4u6ioPmy8ohrBwkQ_a6gNAa9dM7tBhInK9duGt7eNVpZd6Op3l6_WlhmHSJZvyKWut_V_BKO05RRuzpAq3zUOVD25TJkdhARUhJU8KIsLH6PPwkg1P2_NYdZQSCqQISNymaLwP1ChbsBENU_3JcqKriI5lOUgMTi3bGyH-PJ_XdAJbdfBJE1Y8mpBqup-hFNh40HicFZspqU6J9D5jUdKMhpaGhrW51l1f2RHugzKiUjfBs8eIM55_Vj1HeAaXPi23M2-28zF3GLYYysDwk3sQmfwzNeXt6tT6XePX3fTWU2eCw71u1yZkI0gUvgVkwShqlqI-XzzozWekLcbEgN_b0Ij9sYmJWaky0jqYL2oQ8C_UsWXwWx1F0gxYL-k5HDuNKGxC22iLnD_QYXKEKTreoFJvaAzSL0SWirKYSaD1WCVIaScr_gWuea6iXzc371GqLNIRHpRPysIWHJa4tR6gptxisrB1W-Zf_949Xem6ahTmfFi_xC6X-6dYrUO6VKGJVdOhoAMqzP5wqDVnWp_msE9ogYil-TOOrdAAU1H9baSHhp52VZjYRJVdqBf82JJAN1f9YQm8Jak3uqfbcqcxQ8YsMNt7ncL1THdWfvgTzPMFKQ2yJekZpf_f7l1S9cJgLOTkEDU4wN0A1TMVN1zKz8GhVze1aBM6hyMHfUd5IJOE4bex0M3dHn39Qis-mHRdX71LYMCl6fMyjBxDeORpdnys6My_4FrI25F6NPYby_-H7w1qNf1Lcv8A0UGFbQ=w813-h899-no?authuser=0)
11. The waveform should reflect your speech. Next we will try the depth camera
    ```
    freenect-glview
    ```
    You should see this
    (context: You are seeing the three pillars from Mech also all three are Rich and ready to give party at any point of time :yum: )
    
    ![image](https://lh3.googleusercontent.com/KQCrJDsalZQ0QqniPS57g3fXtPTHIj9geCURi9UhxM0HTC3mrPY_sq-MQ6008wHDntWNKaRmc7oIyNaEBuPG0NSdH7J9eTGnLO4atNDKpZLLY88iCKzv5KyPc9YKAUAH1KH5UbaZ3os39Y60AP1P750iS-8RtUxPwqEglpvckYcBYRtZ7B-73PAne0yIzJH1OKEuraj37KwGG1BV0CySHBVhHB-JVCzDByKUxwhPnTagJEuMaZkK1y47-I2xrymjDg8xcbQHazc6GNOOPPMhctM2TkZZW91rGbhf-1Wc7KIvmIf43AG3BuCZYSN6zYIVP89KmuN3lUoXfLqKPEHLcX4bEtaDUvVDxxkuoidVmVpBkkCthZVN3pEhW-CipVpYHCQe8gxJ9tzDqSjIS4edezsZGpTFgPWMzqO5g5AT96wQ8Pkw02pQq4KDqZbSV6UGHQ16OlI046gACbo5cRV3Km2oUhswLJS2OT90di7GPGru-dWgZlFCpIYlCBLLmCcPNrDCbZFO5mMpbUgoBMckgJO9FQn-y1IBh-2YDqpzyUQkm_OQrRaXO0JXcwJx9fWMH1VvgpcGxW_2xjII1DFSWoHfnd0P2RQ5ErNkctWuchN6SUBIZeqDQzzK0qGODgvjXaTxh0L-YukWEksaiROFP1PcBBvk8Unb3M5Y5mTgBLCmJvBJVs-1MP_Q_bSfZ2OXwYEjIiJGoh1u7oxLZkLNLd7lBzat9y13QdpG3tliGm4SFhNDTfY8KNxUX59IVSSGWOLQTzvN-cNhOgR6atimsVVyrQ3e-1H6JwX2Ay54Qaz1fzod_Hm3-aYiUJtT3XMVO7-wPYOsWUUNJjg5WRomgNTQFLi3V5qjh514XhgQHqS0MKVKDLg8oFttKABEruKibuyw5Hpl5ovsPsQRFhK5Nf_96yFqnqM8hiuAab2LMM-y2cKy8Dyk0CqlryaCWgIeW-Up8ErXbLOyybqfm72lJA=w282-h231-no?authuser=0)
12. Also one more bonus you can control the orientation, glowing LED color, change video format, mirror video, and much more. Refer to the screenshot given below.
    ![image](https://lh3.googleusercontent.com/Z9Mz1lU5vmdRxNxl9tzzvKjq7LFxOntHaVdA-jj4cBY_am_ZuFuaYITnDM9RsvmHaGb7c_ba6WEdz_l7iHYELkT702HQKZqZiPj5G0HNafCpshjT0QEm8SfBXVSliXwUEogp7EFZPnIzMHgk12t2NMTyE1InVAHeaxBanEvJrZEBjZJL4UyVwMdfKGT3Y1h3ZDfXRuY43r4NAeBWv-Vtga35WmnzEGZ0bdwWVJnXlUfNuZrFoC-SnrABl1qeXlMBGjeooBUpkYz7zphDz_7tsQNJRhmGhzeBoebUUFfwVFLbxXGw5q-fRtoAB4oE8g25_cWO15RBw9CQuyQez1Skh2KFWP_AlEL_RKdNHNOa50X8xnqkG4WsBI34F9udwHURH-Arl5JTUwUljddznp3CsWN6ya33rgShry-hrJZJKsAdzP_w0CpfkQFe_fj2nvI6VrKR9FyJ_BGK8z9CJs7YF7TMpv77yU__oUPnOFMB8Okf__Cl1eq0jqBY7-fVprvN-i3B8Xyb8pEkqlPI2w7LrGqVrxaH0Mb37tk35YcLJIA1F4CO9qnJfzehbkfsO7s5EyrMdJGlhl71H0u4s6nYOQYO7RSZRZM4u0Zxu6whMBht_GCPs85IyAIHmvqsqgyHSVh4uSYgd6KsfN_F3IqSt13z8K35iSpkAH0UsWN30bRiOAoraaGK7iQ7etUE6J2GXPf_RjeyNwAcByhcTs0Dc-9w7ZbAdt5bSrNay7l2Y0VtVZBHw0WPCS5BL0cOxIdQtir7OTRAQQTq1np2QLKJ6OBvc1IpHlV2omFLeKswwTstzB9VNqZKh6NosL4h8AXSgDhJWkyeFmxD1NRTIgh2l_LG5rucVnBiRo12e6WiXCRnALZBjaO-tby3Zz7vAFGnSO4TFNytzdcR5DZsYhDThf6P_bWAygAZFBuvRytfr8kWF5PSpp5hIY9dRhdBuj7BObon4ovX_HWAlACkaiHrwQ=w936-h61-no?authuser=0)
    To perform these operations you need to select the camera window then click the required key.
13. Congratulations! Our Kinect now works on Ubuntu! Now give party to me this is Manas the GOD :grin: .