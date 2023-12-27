# <img src="https://www.gstatic.com/lamda/images/favicon_v1_150160cddff7f294ce30.svg" width="35px" alt="Bard Icon" /> Reverse Engineered Async API for Google Bard

## Authentication

Go to <https://bard.google.com/>

- F12 for console
- Copy cookie values of `__Secure-1PSID` and `__Secure-1PSIDTS`

## Usage

### Initialization

```python
from src import BardClient

Secure_1PSID = [COOKIE VALUE HERE]
Secure_1PSIDTS = [COOKIE VALUE HERE]

client = BardClient(Secure_1PSID, Secure_1PSIDTS, proxy=None)
await client.init()
```

### One-time Chat

```python
response = await client.generate("Hello World!")
print(response.text)
```

### Chat with Persistent History

```python
chat = client.newchat()
await client.generate("Briefly introduce Europe", chat=chat)
response = await client.generate("What's the population there?", chat=chat)
print(response.text)
```

### Retrieve Images in Response

```python
response = await client.generate("Show me some pictures of cats")
images = response.images
for image in images:
    print(f"{image.alt}({image.url})", "\n")
```

### Check Other Answer Choices

```python
response = await client.generate("What's the best Japanese dish in your mind? Choose one only.")
choices = response.choices
for choice in choices:
    print(choice, "\n----------------------------------\n")
```