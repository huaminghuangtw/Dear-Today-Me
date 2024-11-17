✉️ Dear Today Me
===============

> _“We are what we repeatedly do every day. Excellence, then, is not an act, but a habit.” — Will Durant_  

# About

This repo holds a letter to my present self from Better Me, a reminder for myself to never lose sight of the person I am becoming (and unbecoming). The principles and philosophies in the script are not just words and sentences; they represent the values I believe and strive to live by every single day. These timeless insights and wisdom have been instrumental in shaping my mindset and approach to life. They are the navigation compass that guides me through life's challenges, helping me [stay on course](https://en.wikipedia.org/wiki/1_in_60_rule) toward the true north in this fast-paced world. They also serve as an operating manual whenever I find myself feeling lost.

# Tools

The following tools provided convenient ways to integrate the letter into your daily routine, whether you're commuting, working out, or taking a moment to reflect:

## Apple Shortcuts

[Shortcut Download link]()

The shortcut will play the entire script as speech, acting like a personal life coach in your pocket. Trigger the shortcut manually or integrate it with Siri for hands-free access.

## Scheduled Notifications

[Shortcut Download link]()

Instead of listening to the letter, you can also get scheduled notifications with a random excerpt from the letter at predefined times throughout your day. Go to the "Automation" tab in your Shortcuts app, select this Shortcut, and configure the time and frequency of the notifications based on your preference.

## Scriptable Widgets

It is also possible to displaying a random paragraph from the letter on your Home Screen. Every time you glance at your phone, you'll have a gentle reminder to center your thoughts and actions throughout the day.

### Setup

1. Copy the following JavaScript code into the [Scriptable](https://scriptable.app) app.

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

2. Save the script, then add the widget to your Home Screen.

## Obsidian Dataview

If you are using [Obsidian](https://obsidian.md), this option allows for showing a random paragraph of the letter in your Obsidian vault.

### Setup

1. Make sure you have installed the [Dataview](https://github.com/blacksmithgu/obsidian-dataview) plugin in Obsidian.

   ```dataviewjs
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

2. Copy the following DataviewJS script into the e.g. `Homepage.md` in your Obsidian vault.

===

> [!NOTE]
> We believe in the power of [learning (and building) in public](https://www.swyx.io/learn-in-public). If you have additional life advice (with source link) that you think could fit in the script, feel free to contribute!
>
> [Create a pull request](https://github.com/huaminghuangtw/Dear-Today-Me/compare) with your additions, or [open an issue](https://github.com/huaminghuangtw/Dear-Today-Me/issues/new) to share your ideas, suggestions, or feedback with me!
