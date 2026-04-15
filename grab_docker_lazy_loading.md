🔗 Ref: https://engineering.grab.com/docker-lazy-loading

### COW
A container’s filesystem is made of multiple **read-only layers** from the image. When the container starts, a **writable layer** is added on top.

- Reading a file → comes from existing layers  
- Modifying a file → Docker **creates a copy in the writable layer** and updates that  

The original image layers are **never changed**.

This is called **copy-on-write (CoW)**.

![Architecture](https://github.com/user-attachments/assets/9915ebed-5e3b-41b1-b0f5-4fa3122b9d30)
*Image source: Grab Engineering Blog*

---

### 🧠 Problem (traditional pull)
- Downloads **entire image layers**
- Unpacks everything to disk  
- Builds rootfs  
- **Only then starts container**

👉 Slow for large images (startup delay)

---

### ⚡ Solution (remote snapshotter)
- **Don’t download everything upfront**
- Create a **virtual filesystem** pointing to remote image
- Start container immediately  
- Fetch files **only when accessed**

👉 Faster startup, less waiting

---

### 🎯 One-liner
> Traditional = download first, then run  
> Lazy loading = run first, download as needed
