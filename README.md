✉️ Dear Today Me
===============

> _“We are what we repeatedly do every day. Excellence, then, is not an act, but a habit.” — Will Durant_  

## About

This repo holds a letter to my present self from Better Me, a reminder for myself to never lose sight of the person I am becoming (and unbecoming). The principles and philosophies in the letter are not just words and sentences; they represent the values I believe and strive to live by every single day. These timeless insights and wisdom have been instrumental in shaping my mindset and approach to life. They act as a guiding compass, helping me cut through the noise and navigate chaos, so I can [stay on course](https://en.wikipedia.org/wiki/1_in_60_rule) toward the true north in this fast-paced world. They also serve as a personal operating manual, offering clarity whenever I feel lost amid life's challenges.

## Tools

I built the following tools to provide different ways that integrate the letter into your daily routine, whether you're _commuting_, _working out_, or _taking a moment to reflect_.

### 1. Apple Shortcut

[⤵️ Shortcut Download link](https://www.icloud.com/shortcuts/1013c007965045cc9b0aa39b3a6ff800)

Inspired by [Marcus Aurelius](https://www.goodreads.com/quotes/8177571-at-dawn-when-you-have-trouble-getting-out-of-bed), the shortcut will play the entire script as speech, acting like a personal life coach in your pocket.

#### Setup

1. Click on the Shortcut [download link](https://www.icloud.com/shortcuts/1013c007965045cc9b0aa39b3a6ff800).
2. Tap on **Add Shortcut** to add it to your library.
3. Run the shortcut manually or via Siri for hands-free access.

---

### 2. Scheduled Notification

[⤵️ Shortcut Download link](https://www.icloud.com/shortcuts/7f7303a6f0c64ff1b9a2ff2514b4c0ed)

Instead of listening to the letter, you can also get a scheduled notification with a random excerpt from the letter at predefined times throughout the day.

<p align="center">
  <kbd>
	  <img src="https://github.com/user-attachments/assets/6cf3069b-b62b-450a-8ad4-3ce585343fdb" alt="scheduled-notification" width="400"/>
  </kbd>
</p>

#### Setup

1. [Download the shortcut](https://www.icloud.com/shortcuts/7f7303a6f0c64ff1b9a2ff2514b4c0ed).
2. Launch the Shortcuts app on your iPhone.
3. Navigate to the **Automation** tab at the bottom of the screen.
4. Tap the `+` button in the top-right corner, and choose **Time of Day** to set a specific time and frequency (e.g., _Daily_, _Weekly_).
	* Alternatively, choose **Alarm**, **Wake Up**, or other triggers based on your needs/preference.
5. After selecting the trigger, tap **Next** to proceed to the actions screen.
6. Search for the Shortcut name and select it to run at the scheduled time.

---

### 3. Scriptable Widget

It is also possible to display a random paragraph from the letter on your Home Screen. Every time you glance at your phone, you'll have a gentle reminder to center your thoughts and actions.

<p align="center">
  <kbd>
	  <img src="https://github.com/user-attachments/assets/4e31f8ba-fd2c-46a1-ae63-0e691ff645f3" alt="scriptable-widget" width="600"/>
  </kbd>
</p>

#### Setup

1. Copy the following JavaScript code into the [Scriptable](https://scriptable.app) app by creating a new script (give it a name).

   ```js
   let widget = new ListWidget();

   widget.backgroundColor = new Color("#000000");
   widget.useDefaultPadding();

   let fileContent = await new Request("https://raw.githubusercontent.com/huaminghuangtw/Dear-Today-Me/main/Dear-Today-Me.md").loadString();

   let allParagraphs = fileContent.split("\n\n");

   // Skip salutation and closing lines
   let selectedParagraphs = allParagraphs.slice(1, allParagraphs.length - 2);

   let randomParagraph = getRandomItem(selectedParagraphs);

   let plainTextFromMarkdown = convertMarkdownToPlainText(randomParagraph);

   let text = widget.addText(plainTextFromMarkdown);

   text.centerAlignText();
   text.textColor = new Color("#ffffff");
   // http://iosfonts.com
   text.font = new Font("IowanOldStyle-BoldItalic", 16);
   text.minimumScaleFactor = 0.1;
   text.textOpacity = 1;

   config.runsInWidget ? Script.setWidget(widget) : widget.presentMedium();

   Script.complete();

   // ================
   // Helper funcitons
   // ================

   function getRandomItem(arr) {
      return arr[Math.floor(Math.random() * arr.length)];
   };

   function convertMarkdownToPlainText(markdown) {
      // Convert headings (e.g., "# Heading" to "Heading")
      markdown = markdown.replace(/(^|\n)#+\s*(.+)/g, '$2');

      // Convert links [text](url) to "text"
      markdown = markdown.replace(/\[([^\]]+)\]\([^\)]+\)/g, '$1');

      // Remove bold (**text** or __text__)
      markdown = markdown.replace(/(\*\*|__)(.*?)\1/g, '$2');

      // Remove italic (*text* or _text_)
      markdown = markdown.replace(/(\*|_)(.*?)\1/g, '$2');

      // Remove inline code `code`
      markdown = markdown.replace(/`([^`]+)`/g, '$1');

      // Remove code blocks ```code```
      markdown = markdown.replace(/```[^`]*```/g, '');

      return markdown.trim();
   };
   ```

2. Save the script, then go to Home Screen, long press and add a [Scriptable widget](https://docs.scriptable.app/listwidget) with your preferred size (small, medium, large).
3. Tap on the widget and select the script that you've just created.

> [!TIP]
> _[Check out](https://github.com/huaminghuangtw/Scriptable) my other repository for customizable notifications and widgets created with [Scriptable](https://scriptable.app)!_  

---

### 4. Obsidian's Callout With Dataviewjs

If you are using [Obsidian](https://obsidian.md), this option allows for showing a random paragraph of the letter in a [callout](https://help.obsidian.md/Editing+and+formatting/Callouts) using the [Dataview](https://github.com/blacksmithgu/obsidian-dataview) plugin.

<p align="center">
  <kbd>
	  <img src="https://github.com/user-attachments/assets/31868f8c-291f-41a6-980e-0693184c4445" alt="obsidian-callout-dataview" width="800"/>
  </kbd>
</p>

#### Setup

1. Make sure you have installed the [Dataview](https://github.com/blacksmithgu/obsidian-dataview) plugin in Obsidian.
2. Copy the following [DataviewJS code block](https://blacksmithgu.github.io/obsidian-dataview/queries/dql-js-inline/#dataview-js) into the e.g. `Homepage.md` in your Obsidian vault.

   ```js
   let fileContent = await fetch("https://raw.githubusercontent.com/huaminghuangtw/Dear-Today-Me/main/Dear-Today-Me.md").then(res => res.text());

   let allParagraphs = fileContent.split("\n\n");

   // Skip salutation and closing lines
   let selectedParagraphs = allParagraphs.slice(1, allParagraphs.length - 2);

   let randomParagraph = getRandomItem(selectedParagraphs);

   let callout = `
   > [!QUOTE] ‎
   >> _${randomParagraph}_
   `;

   dv.paragraph(callout);

   // Helper function
   function getRandomItem(arr) {
      return arr[Math.floor(Math.random() * arr.length)];
   };
   ```

## Questions?

* If you need any help with the setup process, feel free to contact me! I will try my best to answer all your questions and look forward to any ideas, suggestions, or feedback that can help improve this project.
* I believe in the power of [learning (and building) in public](https://www.swyx.io/learn-in-public). If you have additional life advice (_with source link_) that you think could fit into the letter, feel free to contribute by _**[creating a pull request](https://github.com/huaminghuangtw/Dear-Today-Me/compare)**_ or _**[opening an issue](https://github.com/huaminghuangtw/Dear-Today-Me/issues/new)**_ to share your additions!  
