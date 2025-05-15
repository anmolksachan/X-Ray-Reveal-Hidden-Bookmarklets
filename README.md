## X-Ray & Reveal Hidden Bookmarklets

A lightweight JavaScript bookmarklets to instantly reveal, enable, and interact with elements that authors have hidden, disabled, or otherwise blocked on a web page—without breaking the site’s layout. Perfect for bug bounty hunters, penetration testers, QA engineers, or curious developers.

---

### 🔍 What Is This?

Modern web apps often “hide” or “disable” form fields, buttons, file upload controls, or UI sections via HTML attributes or CSS rules. While intended to guide user flows, these techniques can mask:

- **Hidden inputs** (e.g. file-upload fields)  
- **Disabled or read-only form elements**  
- **CSS-hidden content** (`display:none`, `visibility:hidden`, `opacity:0`)  
- **Blocked interactions** (`pointer-events:none`)  
- **Collapsed `<details>` tags**  

Both bookmarklets strip out these barriers on demand—letting you inspect, manipulate, or automate interactions with any part of the page.

---

### 🚀 Live Demo

Try it yourself on our demo page:

> **[https://anmolksachan.github.io/](https://anmolksachan.github.io/demo_hidden.html)**

---

## 📜 Bookmarklet Codes

**1. 🛠 Nuclear Reveal Mode**  
- Forces **all** elements visible and interactive, then outlines them in red.

```javascript
javascript:(function(){var css="*{display:block!important;visibility:visible!important;opacity:1!important;pointer-events:auto!important}[hidden]{display:block!important}input[readonly],input[disabled]{background:#fff!important}details,details>summary{display:block!important}",s=document.createElement("style");s.textContent=css,document.head.appendChild(s),document.querySelectorAll("[hidden],[disabled],[readonly]").forEach(function(e){e.removeAttribute("hidden"),e.removeAttribute("disabled"),e.removeAttribute("readonly")}),document.querySelectorAll("details").forEach(function(d){d.open=!0}),document.querySelectorAll("*").forEach(function(e){e.style.outline="2px dashed red"}),alert("🛠%EF%B8%8F Nuclear Reveal Mode Activated!")})();
````

**2. 🚀X-Ray**
- Non-destructive: only removes hiding/disabling attributes and CSS inline rules.

```javascript
javascript:(function(){['hidden','disabled','readonly'].forEach(a=>document.querySelectorAll('['+a+']').forEach(e=>e.removeAttribute(a)));document.querySelectorAll('[style]').forEach(e=>{let s=e.style;if(s.display==='none')s.removeProperty('display');if(s.visibility==='hidden')s.removeProperty('visibility');if(s.opacity==='0')s.removeProperty('opacity');if(s.pointerEvents==='none'){s.removeProperty('pointer-events');s.removeProperty('opacity');}});document.querySelectorAll('details').forEach(d=>d.open=true);alert('✅ Hidden/disabled elements revealed!');})();
```


**3. 🔖 Enable all disabled or readonly fields:**

```javascript
javascript:(function(){document.querySelectorAll('[disabled],[readonly]').forEach(el=>{el.removeAttribute('disabled');el.removeAttribute('readonly');});})();
```

**4. 🔖 Unhide elements styled with display: none:***
```javascript
javascript:(function(){document.querySelectorAll('[style*="display: none"]').forEach(el=>{el.style.display='block';});})();
```

**5. 🔖 Re-enable blocked interactions (pointer-events: none):***
```javascript
javascript:(function(){document.querySelectorAll('[style*="pointer-events: none"]').forEach(el=>{el.style.pointerEvents='auto';el.style.opacity='1';});})();
```

**6. 🚀 All-in-one (For 3,4 & 5):**
```javascript
javascript:(function(){document.querySelectorAll('[disabled],[readonly]').forEach(el=>{el.removeAttribute('disabled');el.removeAttribute('readonly');});document.querySelectorAll('[style*="display: none"]').forEach(el=>{el.style.display='block';});document.querySelectorAll('[style*="pointer-events: none"]').forEach(el=>{el.style.pointerEvents='auto';el.style.opacity='1';});alert('Disabled, readonly, and hidden elements are now active!');})();
```
---

## 🛠️ How to Install

1. **Show your Bookmarks Bar**

   * Windows/Linux: `Ctrl+Shift+B`
   * Mac: `⌘+Shift+B`

   ![image](https://github.com/user-attachments/assets/8e2caa70-c729-4fcf-b628-22bd3f5bc7cb)

2. **Add a New Bookmark**

   * Right-click the bookmarks bar → **Add page…**
   * **Name:** anything (e.g. “X-Ray Debug” or “Reveal Hidden”)
   * **URL:** paste the full one-line bookmarklet code

     ![image](https://github.com/user-attachments/assets/9b46e3aa-2153-4c31-b029-f48e825261e2)
     ![image](https://github.com/user-attachments/assets/cac18d1e-8a87-4883-8177-fe9aaac66c00)
     ![image](https://github.com/user-attachments/assets/15fcd5c5-599c-48e7-964e-50e88c492ec3)

3. **Save** and voilà—click the bookmarklet on any site to activate.
   - 🛠 Nuclear Reveal Mode
   ![image](https://github.com/user-attachments/assets/11d38649-5d79-4f6b-81cb-6c07200f3247)
   ![image](https://github.com/user-attachments/assets/912a99a5-c3ae-42e8-a9e4-db20958ee2a8)

   - 🚀X-Ray
   ![image](https://github.com/user-attachments/assets/f6a905fc-0f7f-4f58-a53a-dba4459b436e)
   ![image](https://github.com/user-attachments/assets/08351c54-e537-4e9f-8d7a-a0585b5030b3)

---

## 💡 Why It Matters

* **Security Testing & Bug Bounties**
  Hidden or disabled fields may expose unguarded server-side endpoints or unvalidated parameters. Quickly reveal and test them.

* **Quality Assurance**
  Validate that hiding logic behaves correctly; catch edge-cases where UX elements become inaccessible.

* **Accessibility & Automation**
  Ensure assistive-tech compatibility or script interactions without manual DOM manipulation.

* **Learning & Debugging**
  Understand how complex web apps structure and hide content; step through every element even in heavily scripted UIs.

---

### 📣 Feedback & Contribution

- Feel free to open issues or pull requests! Whether it’s refinements, new features, or deeper automation—let’s make web testing faster and more transparent.
- Inspired from linkedin post by [André Baptista](https://www.linkedin.com/posts/0xacb_hidden-or-disabled-fields-are-commonly-overlooked-ugcPost-7328708362781511680-houe?utm_source=share&utm_medium=member_desktop&rcm=ACoAABws_M0BR-1VMqnLP2NNWRoOGZSPtyj_R6Y)

---

> *Built by Anmol Sachan 
• [Live demo](https://anmolksachan.github.io/demo_hidden.html) 

**Usage Notes:**
- Each bookmarklet is a self-contained, single line beginning with `javascript:`  
- They do **not** require page reloads and leave non-hidden layout intact (especially the second, “Reveal Hidden Only” version)  
- You can tweak the alert messages, outline colors, or CSS selectors as needed  
