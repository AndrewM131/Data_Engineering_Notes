# Midterm Review

## Hashing 

- Hash functions takes a key and returns ans index into a hash table 
- Generates the unique index corresponding to that value in the hash table 
- Data can be hashed into a shorter fixed lenght value for quicker access using a key or set of characters 
- The representation of the hash function looks like this: `hash = hashfunc(key)`

### How does it work?

- Hash key: the data you want to be hashed
- Types of hash keys:
    - Public key: an open key used solely for data encryption
    - Private key: a symmetric key used for both purposes, encryption and decryption
    - SSH public key: SSH is a set of both public and private keys 
- Hash function: performs a mathematical operation of accepting the key value as input and producing a hash value as the output:
    - Must produce the same hash value for the same hash key to be deterministic 
    - Every input has a unique hash code 
    - It must be collision-friendly
    - A little bit of change leads to a drastic change in the output
    - Calculation must be quick 

### Hash collisions 
- Collisions happen when two or more keys point to the same array index. Chaining, open addressing, and double hashing are a few techniques for resolving collisions.
    - Open addressing: collisions are handled by looking for the following empty space in the table. If the first slot is already taken, the hash function is applied to the subsequent slots until one is left empty. There are various ways to use this approach, including double hashing, linear probing, and quadratic probing.
    - Separate Chaining: In separate chaining, a linked list of objects that hash to each slot in the hash table is present. Two keys are included in the linked list if they hash to the same slot. This method is rather simple to use and can manage several collisions.
    - Robin Hood hashing: To reduce the length of the chain, collisions in Robin Hood hashing are addressed by switching off keys. The algorithm compares the distance between the slot and the occupied slot of the two keys if a new key hashes to an already-occupied slot. The existing key gets swapped out with the new one if it is closer to its ideal slot. This brings the existing key closer to its ideal slot. This method has a tendency to cut down on collisions and average chain length.

### Hash table: fast lookup
- A Hash table is defined as a data structure used to insert, look up, and remove key-value pairs quickly. It operates on the hashing concept, where each key is translated by a hash function into a distinct index in an array. The index functions as a storage location for the matching value. In simple words, it maps the keys with the value.
- For lookup, insertion, and deletion operations, hash tables have an average-case time complexity of O(1). Yet, these operations may, in the worst case, require O(n) time, where n is the number of elements in the table.

### Example of hashing using hashlib 

```

import hashlib

def sha256(input):
    hash_object = hashlib.sha256(input.encode('utf-8'))
    hex_digest = hash_object.hexdigest()
    return hex_digest

def main():
    message = "Hello, world!"
    hash_value = sha256(message)
    
    print("Message: " + message)
    print("SHA-256 Hash: " + hash_value)

if __name__ == "__main__":
    main()
```

Output:
```
Message: Hello, world!
SHA-256 Hash: 315f5bdb76d078c43b8ac0064e4a0164612b1fce77c869345bfc94c75894edd3 
```

### Types of hash functions 

1. Division Method 
Formula: `h(k) = k % M` where `k = key value` and `M = size of the hash table`

Example:
```
k = 1987 
M = 13h(1987) = 1987 % 1 3
h(1987) = 4
```

### Asymmetric Key Cryptography 

- A type of encryption that uses a pair of keys to encrypt and decrypt data 
- The pair of keys includes a public key, which cna be shared with anyone, and a private key which is kept secret by the owner 
- Let's consider a scenario: A sender uses the recipient's public key to encrypt the data. The recipient then uses their private key to decrypt the data. This approach allows for secure communication between two parties without the need for both parties to have the same secret key. 
- Sender (uses recipient's public key to encrypt) ---> sends encrypted email --> recipient (uses their own private key to decrypt the email) --> the recipient can now read it 
- The private key is a separate key from the public key that is kept private by the owner of the public key while the public key is made available to everyone 
- Anyone therefore can encrypt a message using a public key but only the holder of a private key can unlock it

- Advantages over symmetric key cryptography:
    - Eliminates the need to exchange secret keys which can be a challenging process if communicating with multiple parties
    - Allows for creation of digital signatures 
    - Providers a higher level of security because it is harder for an attacker to intercept and decrypt the data 
- Disadvantages over symmetric key cryptography:
    - Slower than symmetric encryption because it involves more complex mathematical operations. This can make it less suitable for applications that require fast data processing.
- Example:  Let’s say Alice and Bob have a public-private key pair and Alice wishes to send Bob an encrypted message. Using Bob’s public key, Alice encrypts her message before sending it to him. Bob uses his private key to decrypt the message after receiving it encrypted. For instance, Alice composes and encrypts an email for Bob using Bob’s public key. She follows up by sending Bob the encrypted email. After receiving the email, Bob uses his private key to decrypt it so that it may be read. As a result, Alice can communicate Bob securely without being concerned that the message’s content will be viewed by someone else.

### Symmetric Key Cryptography 

- Symmetric key encryption is where the same keys are used for data encryption and decryption
- One-time pad (OTP): A theoretically impossible cipher where the key is a random string of characters as long as the message itself. The key is used for a single encryption and then discarded.
- Advantages:
    - Speed and efficiency: Symmetric key+ algorithms are better suited for encrypting large volumes of data or for use in real-time communication scenarios as they are faster and less resource-intensive than asymmetric cryptography. SKC algorithms do not involve algebraically mathematical operations.
    - Scalability: Because symmetric key algorithms have relatively low computational overhead, they scale well with the number of users and the amount of data being encrypted.
    - Simplicity: Symmetric encryption protocols are often more straightforward to implement and understand than asymmetric key methods, and this would go a long way in attracting developers and users. 
- Disadvantages:
    - Key management and distribution: Both the sender and the receiver in the SKC of a message need to have the same key, and the key should not be seen by a third party. In case the key is somehow captured or compromised by a third party, the security of the encrypted data is also lost.
    - Non-repudiation: Non-repudiation refers to the ability to prove that a specific party has sent a message. In SKC, since the same key is used for encryption and decryption, it is impossible to find out which party created a particular cipher text.
- Example: Let’s say Alice and Bob share a secret key and Alice wishes to send Bob an encrypted message. Using the shared secret key, Alice encrypts her message before sending it to him. Bob uses the same secret key to decrypt the message after receiving it encrypted. For instance, Alice composes and encrypts an email for Bob using the shared secret key. She follows up by sending Bob the encrypted email. After receiving the email, Bob uses the shared secret key to decrypt it so that it may be read. As a result, Alice can communicate with Bob securely, but both must ensure that the shared secret key remains confidential.

### How does a cryptographic key work?
- Cryptography technique is use to convert plain text into ciphertext. Basically crytographic key is a string of characters which is used to encrypt and decrypt the data 
```
"Gio is cool" + key = "HYMeAS90#"
```


## Imprecise matching

### Jaccard similarity

- Defined as the size of the intersection divided by the size of the union
- Example below:
    - Sentence 1: AI is our friend and it has been friendly 
    - Sentence 2: AI and humans have always been friendly
    - The similarity calculation:
        - S1 (3): our is it
        - S2 (2): human always
        - S1 & S2 (5): AI has been friend and
        - Calculation: 5 / (5 + 3 + 2) = 0.5 
- Flaws:
    - As size of document increases, the size of the common words also does 
    - Does not capture semantic similarity
    - The order of the words does not impact words such as character n-grams 

### Levenstein distance 

- Edit distance is a way to measure how dissimilar two sequences are to each other by counting the minimum number of opertations required to transform sequence into another
- Popular in fuzzy matching where a small number of differences are allowed
- However, computationally expensive to calculate long distances for long sequences

### N-gram similarity
- Definition: N-gram similarity measures the similarity between two sequences by comparing their n-grams (subsequences of length n). It captures the local sequence similarity and is useful for tasks like text matching and plagiarism detection.
- Advantages:
    - Captures local sequence similarity, making it effective for detecting small changes or variations in text.
    - Can handle different types of data, including text, DNA sequences, and more.
    - Flexible in terms of the value of n, allowing for fine-tuning based on the specific use case.
    - Robust to minor errors or variations in the sequences being compared.
- Disadvantages:
    - Computationally expensive for large values of n or long sequences.
    - May not capture global sequence similarity effectively.
    - Sensitive to the choice of n, which can impact the accuracy of the similarity measure.
- Example function:
```python
def ngram(sentence, num):
    tmp = [] 
    sent_len = len(sentence) - num +1
    for i in range(sent_len):
        tmp.append(sentence[i:i+num]) 
    return tmp
```
- This ‘ngram’ function takes two inputs, sentence and the ’N’, for N-gram. If we say 2-grams, a sentence, ‘A cat sat on a mat.’ be fed into this function, the decomposed would be [‘A ‘, ‘ c’, ‘ca’, ‘at’, ‘t ‘, ‘ s’, ‘sa’, ‘at’, ‘t ‘, ‘ o’, ‘on’, ‘n ‘, ‘ a’, ‘a ‘, ‘ m’, ‘ma’, ‘at’, ‘t.’].

```python
def diff_ngram(sent_a, sent_b, num):
    a = ngram(sent_a, num)
    b = ngram(sent_b, num) 
    common = [] 
    cnt = 0 
    for i in a:
        for j in b:
            if i == j:
                cnt += 1
                common.append(i)
    return cnt/len(a), common
```

- We build another function which uses the previous function we just built, the ‘ngram()’. By using ‘ngram()’ function, we decompose each input sentence into N-gram way, and store the decomposed ones in each variable ‘a’, ‘b’. Now, check whether those two lists contain same components. If they have one, then counter, which named under ‘cnt’, will gain 1, and the component will be appended into the list variable ‘common’. To quantify similarity, we divide ‘cnt’ by length of the list ‘a’. Also we return the common component list.

### Semantic embeddings
- Definition: Semantic embeddings are vector representations of words, phrases, or sentences that capture their meanings based on their context in large text corpora. These embeddings are generated using machine learning models like Word2Vec, GloVe, or BERT, and they enable the comparison of semantic similarity between different pieces of text.

- Advantages:
    - Captures semantic meaning: Embeddings can capture the contextual meaning of words, allowing for more accurate similarity comparisons.
    - Handles synonyms: Words with similar meanings have similar embeddings, making it easier to identify synonyms.
    - Supports various NLP tasks: Useful for tasks like text classification, sentiment analysis, and machine translation.
    - Reduces dimensionality: Embeddings provide a compact representation of text, reducing the dimensionality of the data.

- Disadvantages:
    - Requires large datasets: Training embeddings requires large text corpora to capture meaningful relationships.
    - Computationally intensive: Generating embeddings can be resource-intensive, especially for large models like BERT.
    - May not capture rare words: Embeddings may not be accurate for rare or domain-specific words not well-represented in the training data.

- Example using Word2Vec:
```python
from gensim.models import Word2Vec

# Sample sentences
sentences = [
    ["I", "love", "machine", "learning"],
    ["Natural", "language", "processing", "is", "fun"],
    ["Word2Vec", "creates", "word", "embeddings"]
]

# Train Word2Vec model
model = Word2Vec(sentences, vector_size=100, window=5, min_count=1, workers=4)

# Get embedding for a word
word_embedding = model.wv['machine']
print("Embedding for 'machine':", word_embedding)

# Calculate similarity between words
similarity = model.wv.similarity('machine', 'learning')
print("Similarity between 'machine' and 'learning':", similarity)
```
Output:
```python
Embedding for 'machine': [ 0.00123456, -0.00234567, ... ]  # Example vector values
Similarity between 'machine' and 'learning': 0.87654321  # Example similarity score
```

### Password Hashing with Salt

- Password hashing with salt is a technique used to enhance the security of stored passwords by adding a unique random value (salt) to each password before hashing it.
- This approach helps to prevent attacks such as rainbow table attacks, where precomputed hash values are used to crack passwords.

#### How does it work?

1. Generate a random salt for each password.
2. Combine the salt with the password.
3. Hash the combined value using a cryptographic hash function.
4. Store the salt and the hashed value together in the database.

#### Example using Python's `hashlib` and `os` modules:

```python
import hashlib
import os

def hash_password(password):
    # Generate a random salt
    salt = os.urandom(16)
    # Combine the salt with the password
    salted_password = salt + password.encode('utf-8')
    # Hash the combined value
    hash_object = hashlib.sha256(salted_password)
    hash_value = hash_object.hexdigest()
    # Return the salt and the hashed value
    return salt, hash_value

def verify_password(stored_salt, stored_hash, password):
    # Combine the stored salt with the provided password
    salted_password = stored_salt + password.encode('utf-8')
    # Hash the combined value
    hash_object = hashlib.sha256(salted_password)
    hash_value = hash_object.hexdigest()
    # Compare the stored hash with the newly computed hash
    return hash_value == stored_hash

def main():
    password = "securepassword123"
    salt, hashed_password = hash_password(password)
    
    print("Salt:", salt)
    print("Hashed Password:", hashed_password)
    
    # Verify the password
    is_valid = verify_password(salt, hashed_password, password)
    print("Password is valid:", is_valid)

if __name__ == "__main__":
    main()
```

Output:
```
Salt: b'\x12\x34\x56\x78\x9a\xbc\xde\xf0...'  # Example salt value
Hashed Password: 5e884898da28047151d0e56f8dc62927b...  # Example hash value
Password is valid: True
```

- Advantages:
    - Enhances security by adding randomness to each password hash.
    - Prevents the use of precomputed hash tables (rainbow tables) for cracking passwords.
    - Makes it more difficult for attackers to crack multiple passwords at once.

- Disadvantages:
    - Requires additional storage for the salt values.
    - Slightly increases the complexity of the password hashing and verification process.


##  Quantifying server-client performance: throughput, latency and bandwidth

- Latency refers to the time it takes for a packet of data to traverse from one point in the network to another. It is a measure of delay experienced by the packet, indicating the speed in which the data travels across the network. Latency is often measured as round trip time which includes the time for the packet to travel from its source to its destination and for the source to receive the response. A network with low latency experiences less delay thereby feeling faster to the end user.
    - Several factors can influence latency, including:
        - Distance: The physical distance between the source and destination significantly affects latency. Data packets travel through various mediums (e.g., cables), and the farther they have to go, the more time it takes.
        - Network congestion: Congestion in a network can cause delays and increase latency, akin to how traffic congestion slows down vehicle movement.
        - Hardware and infrastructure: The performance and efficiency of network hardware, such as routers and switches, as well as the quality of the network infrastructure, can impact latency.
        - Transmission mediums: The medium of data transmission, whether it’s fiber optic cables, copper cables, or wireless signals, also influences latency (e.g., fiber optic cables typically offer lower latency than other mediums).
        - Number of hops: Each time a data packet passes from one network point to another, it’s considered a “hop.” More hops mean that data packets have more stops to make before reaching their destination, which can increase latency. The number of hops a packet makes can change based on the network’s configuration, topology, and path chosen for data transfer.
        - Latency is typically measured in milliseconds (ms) and can be evaluated using methods like ping and traceroute tests. These tests send a message to a destination and measure the time it takes to receive a response.

- Throughput, on the other hand, is the amount of data that successfully travels through the network over a specified period. It reflects the network’s capacity to handle data transfer, often seen as the actual speed of the network. Throughput depends on several factors, including the network’s physical infrastructure, the number of concurrent users, and the type of data being transferred.
    - It is often measured in bits per second (bps), kilobits per second (Kbps), megabits per second (Mbps), or gigabits per second (Gbps). High throughput means more data can be transferred in less time, contributing to better network performance and a smoother user experience.
    - Several factors can influence throughput, including:
        - Bandwidth: Bandwidth is the maximum capacity of a network connection to transfer data. Higher bandwidth typically enables higher throughput. However, bandwidth is only a potential rate, and the actual throughput could be lower due to other factors.
        - Latency: Higher network latency can reduce throughput because it takes longer for data packets to travel across the network.
        - Packet loss: When data packets fail to reach their destination, the sending device often needs to resend them, which can lower the overall throughput.
        - Network congestion: When many data packets are trying to travel over the network simultaneously, it can lead to congestion and a decrease in throughput.
        - Hardware and infrastructure: The performance and efficiency of network hardware, such as routers and switches, can impact throughput.
    
- Bandwidth is the maximum data transfer capacity of a network. It defines the theoretical limit of data that can be transmitted over the network in a given time. Bandwidth is often compared to the width of a road, determining the maximum number of vehicles (or data packets in a network) that can travel simultaneously.
    - Bandwidth is typically measured in bits per second (bps), with modern networks often operating at gigabits per second (Gbps) or even terabits per second (Tbps) scales. This measurement describes the volume of data that can theoretically pass through the network in a given time frame.

##  Filesystem: directories, paths, filenames and basic file permissions (chmod)
- Key directories include:
    - `/bin`: Essential command binaries.
    - `/etc`: System configuration files.
    - `/home`: User home directories.
    - `/var`: Variable data files.
    - Paths specify the location of files or directories. An absolute path starts from the root directory (e.g., /home/user/documents), while a relative path is defined concerning the current directory (e.g., documents/report.txt). 
- Filenames in Linux are case-sensitive and can include letters, numbers, and special characters, except for the null character (\0) and the forward slash (/). It's advisable to avoid spaces and special characters to prevent potential issues. 
- Linux employs a permission system to control access to files and directories. Each file has three types of permissions:
    - Read (r): View the contents.
    - Write (w): Modify the contents.
    - Execute (x): Run the file as a program.
    - These permissions are assigned to three categories:
        - Owner (user): The file's creator.
        - Group: Users who are part of the file's group.
        - Others: All other users.
        - Permissions can be viewed using the ls -l command, which displays them in a string like -rwxr-xr--. This string represents the file type and permissions for the owner, group, and others, respectively. 

- The chmod command is used to change file permissions. Permissions can be set using symbolic or numeric modes:
    - Symbolic Mode:
        - Add execute permission for the owner: `chmod u+x` filename
        - Remove write permission for others: `chmod o-w `filename
    - Numeric Mode:
        - Permissions are represented by numbers:
            - Read (r) = 4
            - Write (w) = 2
            - Execute (x) = 1
            - Combine these to set permissions. For example, to set read, write, and execute permissions for the owner (4+2+1=7), read and execute for the group (4+1=5), and read-only for others (4), use: chmod 755 filename

