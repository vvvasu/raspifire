---
title: 'Symmetric Encryption: An Uncommon Concept'
author: Vishwa Vasu
type: post
date: 2023-01-18T17:26:45+00:00
url: /encrypted_canbus/
featured_image: /wp-content/uploads/2023/01/symmetric-encryption-high-resolution-logo-480x360.png
nimbo_mb_gallery_thumb_type:
  - slider
nimbo_mb_video_thumb_type:
  - iframe
nimbo_mb_audio_thumb_type:
  - iframe
nimbo_mb_link_target:
  - blank
categories:
  - Cryptography
  - Symmetric Encryption
tags:
  - automotivecryptography
  - automotivesecurity
  - canbus
  - cryptography
  - decryption
  - ecu
  - symmetricencryption

---
<blockquote class="wp-block-quote is-style-plain has-small-font-size is-layout-flow wp-block-quote-is-layout-flow" style="font-style:normal;font-weight:300">
  <p class="has-vivid-red-color has-text-color has-small-font-size">
    Attention: This is just a Python program. No Micro Controllers have been used and non of the functions are related to mechatronics or electronics. Cyber security enthusiasts are welcome to read the blog and super technical visitors are welcome to ignore the following blog.
  </p>
  
  <p class="has-small-font-size">
    This is an experiment to make awareness of how the CAN-BUS messages can encrypt with symmetric cryptographic functions.
  </p>
  
  <p class="has-small-font-size">
    This program is coded with simple python scripts. You can get a basic idea of how a pre-coded 8-byte, raw CAN Message could encrypt using a cryptographic method.
  </p>
</blockquote>

You have probably heard about hacking. And you know networks, systems, and software can be hackable. Have you ever thought a vehicle could be hacked?  
Modern vehicles, such as smart cars, consist of systems, software and networks. Therefore, the vehicles are also hackable if they become vulnerable. This blog is about a security issue in the CAN-BUS of a vehicle. 

Before jumping into CAN-Bus, consider what an ECU is in a vehicle.

## Electronic Controller Unit {.wp-block-heading}

<div class="wp-block-media-text alignwide is-stacked-on-mobile">
  <figure class="wp-block-media-text__media"><img loading="lazy" decoding="async" width="826" height="620" src="https://vazdefense.com/wp-content/uploads/2022/09/Picture1.jpg" alt="Electronic Controller Unit" class="wp-image-95 size-full" srcset="https://vazdefense.com/wp-content/uploads/2022/09/Picture1.jpg 826w, https://vazdefense.com/wp-content/uploads/2022/09/Picture1-300x225.jpg 300w, https://vazdefense.com/wp-content/uploads/2022/09/Picture1-768x576.jpg 768w" sizes="(max-width: 826px) 100vw, 826px" /></figure>
  
  <div class="wp-block-media-text__content">
    <p>
      ECU is Electronic Controler Unit. It is an embedded computer in a vehicle to control mechanics, electronics, or subsystems. It is an electronic component that takes input from its sensor or other ECUs and uses actuators to control the vehicle&#8217;s functionalities.
    </p>
  </div>
</div>

## CAN, aka Controller Area Network {.wp-block-heading}

It&#8217;s a communication protocol such as LAN or WAN. This protocol was standardized by ISO 11898 and ISO 11519. It focuses on the first and second layers of OSI reference mode. Communication over the CAN bus is done via CAN frames.

#### Standard CAN frame {.wp-block-heading}<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="798" height="257" src="https://vazdefense.com/wp-content/uploads/2022/09/Screenshot-2022-09-24-234936.png" alt="" class="wp-image-97" srcset="https://vazdefense.com/wp-content/uploads/2022/09/Screenshot-2022-09-24-234936.png 798w, https://vazdefense.com/wp-content/uploads/2022/09/Screenshot-2022-09-24-234936-300x97.png 300w, https://vazdefense.com/wp-content/uploads/2022/09/Screenshot-2022-09-24-234936-768x247.png 768w" sizes="(max-width: 798px) 100vw, 798px" /> </figure> 

<ul class="wp-block-list">
  <li>
    Data:&nbsp;Contains the data bytes, aka payload, which includes CAN signals that can be extracted and decoded for information
  </li>
</ul>

Vehicles with this technology generate CAN messages when they get the signals from their inputs, such as starting the engine, switching on/off lights, increasing/decreasing gas or brake paddles, etc&#8230;

#### CAN data example {.wp-block-heading}<figure class="wp-block-table">

<table>
  <tr>
    <td>
      <strong>CAN raw data</strong>
    </td>
    
    <td>
      <strong>After decode</strong>
    </td>
  </tr>
  
  <tr>
    <td>
      FF FF FF 68 13 FF FF FF
    </td>
    
    <td>
      Engine speed 621 rpm
    </td>
  </tr>
</table></figure> 

<div class="wp-block-columns is-layout-flex wp-container-core-columns-is-layout-1 wp-block-columns-is-layout-flex">
  <div class="wp-block-column is-layout-flow wp-block-column-is-layout-flow" style="flex-basis:100%">
    <h2 class="wp-block-heading">
      How CAN messages could be hacked?
    </h2>
    
    <ul class="wp-block-list">
      <li>
        CAN is an insecure low-level protocol
      </li>
      <li>
        Every message is an unencrypted, plain-text broadcast to every device(ECU) in the vehicle.
      </li>
      <li>
        Possible messages and communication procedures are often documented and made available freely &#8211; CAN DBC.
      </li>
      <li>
        An external device can send commands.
      </li>
    </ul>
  </div>
</div>

This is the place where **cryptography** in cyber security comes into play.

Cryptography is simply converting a human-readable message, we call it a plain text message, into something unreadable, gibberish text. We call that text ciphertext.

## Symmetric Key Cryptography {.wp-block-heading}

Some algorithms in cryptography can be broken into categories. One is symmetric key cryptography. Here, we use the terms encryption and decryption. In simple words, encryption is keeping secrets. That means converting clear text into ciphertext. And decryption is revealing secrets. It means returning the clear text, the human-readable message from cypher or secret messages.

You encrypt your original data in a symmetric key with a secret key (mathematic algorithm). And you have to keep this private key with you. Then, you can send your data to another party. The recipient of that message has to use the same key that you have to decrypt the secret message. This is called symmetric key encryption. Here, it uses the same key for both encryption and decryption.

## Symmetric Key Cryptography in the Automotive Industry {.wp-block-heading}

<ul class="wp-block-list">
  <li>
    The same key is stored on all interconnected ECUs.
  </li>
  <li>
    AES 128-bit key algorithm
  </li>
</ul>

– Key Generation

<ul class="wp-block-list">
  <li>
    Random keys generated with approved random bit generators (RBG)
  </li>
  <li>
    Using approved cryptographic modules (ECU hardware)
  </li>
  <li>
    It has country-specific compliance standards.
  </li>
  <li>
    USA: FIPS 140-2 compliancy &#8211; National Institute of Standards and Technology (NIST) standards &#8211; Section 4.7.3 <ul class="wp-block-list">
      <li>
        Only approved key establishment methods shall be used if a cryptographic module employs key establishment methods.
      </li>
      <li>
        Compromising the security of the key establishment method (e.g., compromising the security of the algorithm used for key establishment) shall require at least as many operations as determining the value of the cryptographic key being transported or agreed upon.
      </li>
    </ul>
  </li>
  
  <li>
    Europe: European Union Agency for Network and Information Security (ENISA) Chapter 2 in &#8220;Algorithms- key size and parameters&#8221;
  </li>
</ul>

– Key Distribution

<ul class="wp-block-list">
  <li>
    Primary ECU as key management server(KMS)
  </li>
  <li>
    Responsible for the generation and distribution of secret keys
  </li>
  <li>
    Distribution via PDUs, network agnostic
  </li>
  <li>
    Distribution in the production phase (secure premises)
  </li>
  <li>
    Default key installed in ECUs on initialization
  </li>
  <li>
    After the first distribution, key updates require the previous key.
  </li>
  <li>
    Key data encrypted with older key
  </li>
  <li>
    Keys installed and activated on reception from KMS
  </li>
  <li>
    It is stored in and accessed from secure on-chip hardware.
  </li>
</ul>

&#8211; Archiving and Destroying old keys

<ul class="wp-block-list">
  <li>
    Keys have a lifespan of 30 days
  </li>
  <li>
    KMS distributes new keys to all ECUs
  </li>
</ul>

## Why use Symmetric Key instead of other cryptographic functions for CAN message encryption? {.wp-block-heading}

<p class="has-small-font-size">
  <strong>Symmetric key</strong><br />Efficiency and speed of execution. Bulk data to be encrypted.<br />Example: Freescale&#8217;s AES-128 hardware accelerator on the MPC5646C (microprocessor) device can execute at 70 MB/s.
</p>

<p class="has-small-font-size">
  <strong>Asymmetric key</strong><br />Asymmetric key encryption has limitations. A relative increase in computation time for RSA authentication using a public key. (More than 100 MB/s)
</p>

## Instruction for the code deployment {.wp-block-heading}

<ul class="wp-block-list">
  <li>
    Import the following modules to your IDE: <ul class="wp-block-list">
      <li>
        &#8220;python-can&#8221; &#8211; <a rel="noreferrer noopener" href="https://pythoncan.readthedocs.io/en/master/installation.html" target="_blank">https://pythoncan.readthedocs.io/en/master/installation.html</a>
      </li>
      <li>
        &#8220;cryptography&#8221; &#8211; <a rel="noreferrer noopener" href="https://cryptography.io/en/latest/" target="_blank">https://cryptography.io/en/latest/</a>
      </li>
    </ul>
  </li>
  
  <li>
    Create a Virtual CAN adapter &#8211; refer to the &#8220;automatecanopen.py.&#8221;
  </li>
  <li>
    Run the CAN receiver, then the CAN sender <ul class="wp-block-list">
      <li>
        CAN receiver &#8211; ecu_2.py
      </li>
      <li>
        CAN sender &#8211; ecu_1.py
      </li>
    </ul>
  </li>
</ul>

#### automatecanopen.py {.wp-block-heading}

<p class="has-small-font-size">
  This creates a virtual CAN socket to send and receive CAN data.
</p>

<pre class="wp-block-code has-cyan-bluish-gray-color has-black-background-color has-text-color has-background has-small-font-size"><code>import subprocess


subprocess.call('sudo modprobe vcan', shell=True)
subprocess.call('sudo ip link add dev vcan0 type vcan', shell=True)
subprocess.call('sudo ip link set up vcan0', shell=True)</code></pre><figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="377" height="322" src="https://vazdefense.com/wp-content/uploads/2022/09/Screenshot-2022-09-25-183115.png" alt="" class="wp-image-135" srcset="https://vazdefense.com/wp-content/uploads/2022/09/Screenshot-2022-09-25-183115.png 377w, https://vazdefense.com/wp-content/uploads/2022/09/Screenshot-2022-09-25-183115-300x256.png 300w" sizes="(max-width: 377px) 100vw, 377px" /> </figure> 

<p class="has-small-font-size">
  You can test the CAN socket using candump and cansend commands.
</p>

#### ecu_1.py {.wp-block-heading}

<p class="has-small-font-size">
  I&#8217;m going to send the &#8220;[0, 25, 0, 1, 3, 1, 4, 1]&#8221; Hexa array via the CAN socket(&#8220;vcan0&#8221;) that I created in the first Python script. After running this script, I encrypted this hex array with the symmetric key I generated and stored in the &#8220;keystorage.txt&#8221;.
</p>

<pre class="wp-block-code has-cyan-bluish-gray-color has-black-background-color has-text-color has-background has-small-font-size"><code>import can
from cryptography.fernet import Fernet
from can import Message

bus = can.interface.Bus(bustype='socketcan', channel='vcan0', bitrate=2500000)

#Key Generation

key = Fernet.generate_key()
fkey = open("keystorage.txt",'wb')
w = fkey.write(key)
print('-* Key is generated')
#print("Key is ",key)
cipher = Fernet(key)

#Encryption

##hexa array to be sent on can data frame
message = bytearray(&#91;0, 25, 0, 1, 3, 1, 4, 1])
#print("Original data without encryption : ",message)
##hexa convert into string and encode
message_string = ' '.join(map(str, message)).encode()
#print("Bytearray after encode : ",message_string)
##message_string after encryption
encrypted_msg = cipher.encrypt(message_string)

fkey = open("keystorage.txt","rb")
key2 = fkey.read()
cipher = Fernet(key2)
#originalmsg = cipher.decrypt(msg1)
print("\n")
print("Encypted msg : " ,encrypted_msg)
print("\n")

##split encrypted msg to 8 string charaters
info = &#91;encrypted_msg&#91;i:i+8] for i in range(0, len(encrypted_msg), 8)]
split_string = encrypted_msg.decode()

##string convert into hexa
hex_data = &#91;ord(c) for c in split_string]


#newmessage = hex_data&#91;0:8]
def split_list(lst,n):
    result = list((lst&#91;j:j+n] for j in range (0, len(lst),n)))
    return result
n = 8
encrypted_data = split_list(hex_data,n)
#print(encrypted_data)

try:
    for enc_data in encrypted_data:

        data = Message(data=enc_data)
        bus.send(data)

    print("Message sent on {}" .format(bus.channel_info))
    print("\n")

except can.CanError:
    print(can.CanError)</code></pre><figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="1140" height="171" src="https://vazdefense.com/wp-content/uploads/2022/09/Screenshot-2022-09-25-183931-1.png" alt="" class="wp-image-141" srcset="https://vazdefense.com/wp-content/uploads/2022/09/Screenshot-2022-09-25-183931-1.png 1140w, https://vazdefense.com/wp-content/uploads/2022/09/Screenshot-2022-09-25-183931-1-300x45.png 300w, https://vazdefense.com/wp-content/uploads/2022/09/Screenshot-2022-09-25-183931-1-1024x154.png 1024w, https://vazdefense.com/wp-content/uploads/2022/09/Screenshot-2022-09-25-183931-1-768x115.png 768w" sizes="(max-width: 1140px) 100vw, 1140px" /> </figure> 

<p class="has-small-font-size">
  Run the ecu_2.py before the ecu_1.py script. As you can see, a symmetric key has been generated, and the original data is encrypted into secret data.
</p>

#### ecu_2.py {.wp-block-heading}

<p class="has-small-font-size">
  This is the receiver. This script gets the secret CAN message via &#8220;vcan0&#8221; and generates a random CAN message with secret values, and at the end, it uses the same symmetric key to decrypt the secret CAN message to the original CAN message, which is &#8220;[0, 25, 0, 1, 3, 1, 4, 1]&#8221;.
</p>

<pre class="wp-block-code has-cyan-bluish-gray-color has-black-background-color has-text-color has-background has-small-font-size"><code>import can
from cryptography.fernet import Fernet

bus = can.interface.Bus(bustype='socketcan', channel='vcan0', bitrate=2500000)


message_string = ""
encrypted_data = ""
rmessage = &#91;]

while True:
    message = bus.recv()

    def fullmessage():

        encrypted_msg = message
        print(encrypted_msg)

    fullmessage()

    #Decryption
    def decrypted_data():

        msg_decode = message.data.decode()
        rmessage.append(msg_decode)

        message_string = ''.join(map(str,rmessage))
        #print(rmessage)
        encrypted_data = message_string
        if len(encrypted_data) == 120:

            enc_msg = encrypted_data.encode()
            print("\n")
            print("Encrypted msg : ",enc_msg)
            fkey = open("keystorage.txt", 'rb')
            key = fkey.read()
            #fkey.close()

            cipher = Fernet(key)

            original_data = cipher.decrypt(enc_msg)
            byte_array = (&#91;original_data])
            print("\n")
            print("This is the original data frame : ",byte_array)
            print("\n")

    decrypted_data()
</code></pre><figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="1212" height="438" src="https://vazdefense.com/wp-content/uploads/2022/09/Screenshot-2022-09-25-190321.png" alt="" class="wp-image-155" srcset="https://vazdefense.com/wp-content/uploads/2022/09/Screenshot-2022-09-25-190321.png 1212w, https://vazdefense.com/wp-content/uploads/2022/09/Screenshot-2022-09-25-190321-300x108.png 300w, https://vazdefense.com/wp-content/uploads/2022/09/Screenshot-2022-09-25-190321-1024x370.png 1024w, https://vazdefense.com/wp-content/uploads/2022/09/Screenshot-2022-09-25-190321-768x278.png 768w" sizes="(max-width: 1212px) 100vw, 1212px" /> </figure> 

<p class="has-small-font-size">
  As you can see, the encrypted hex array(CAN message) is transferred as random messages(8-byte data) through the CAN socket, and the original message has been decrypted using the same symmetric key and shows the original Hexa array.
</p>