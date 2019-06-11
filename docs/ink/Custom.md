# Custom
To make your Ink script more interesting and multimedia-ready, you can add [metadata cues](#metadata) and [fancy styling](#styling).

## Metadata

- `# char: player, npc` specifies who is speaking, so we can pull the correct dialogue box assets
- `# mood: happy` specifies which facial expression a character should display
- `# sfx: crash --before` specifies the sound to play before this line of text
- `# sfx: crash --after` specifies the sound to play after this line of text
- `# style: MyLabel <color=red><sprite name=Misc></color>` specifies a custom style to apply to any text surrounded by `<style=MyLabel></style>`

## Styling

### Built-In Styles
If you need a style that won't be repeated very often or doesn't require a lot of decoration, you can use any of the tags provided by [TextMesh Pro's Rich Text](http://digitalnativestudios.com/textmeshpro/docs/rich-text/). For example:
- `<i>Italicized Text</i>` for *Italicized Text*
- `<s>Strikethrough Text</s>` ~~for Strikethrough Text~~
- `<u>Underlined Text</u>` for <u>[Underlined Text]</u>
- `<b>Bold Text</b>` for **Bold Text**
- `<noparse><b></noparse>` to show `<b>` instead of **b**
- `<nobr>Stay Together<nobr>` to prevent the words `Stay Together` from being split onto separate lines by word wrapping.
- `<sprite name=Smiley>` to insert a custom emoji named `Smiley` such as 🙂 (Remember to give these emoji images to a dev!)

### Custom Styles
Group together several style formats under a single label to stylize dialogue your INK script:
- `<style=Label>Text</style>` applies the style labeled `Label` to `Text`
- Use the label `Person` for text representing a character's name 
- Use the label `Place` for text representing an in-game location
- Use the label `KeyItem` for text representing a key item
- Use the label `Hint` for text that is an important clue
- Use the label `Money` for text representing a sum of money
- Use the label `Time` for text representing in-game time
- Use the label `Loud` for text that represents a loud sound or voice
- Use the label `Whisper` for text that represents a soft or whispered voice

![styles preview](/docs/img/FormatStyles-cropped.png)

Create your own label if you need one that isn't listed here. You can write it as a comment near the top of your main INK script: `# style: MyLabel <color=red><sprite name=Misc></color>`

**Note 1:** Custom styles can't be made to automate progressively shrinking or expanding text. This sort of functionality is programmable, but should be considered a "nice-to-have" and not a requirement. Unless you need to use it often, you'll have to make do with stuff like `<size=100%>Echo <size=80%>Echo <size=60%>Echo <size=40%>Echo <size=20%>Echo`

**Note 2:** TextMesh Pro's rich text styles won't work on custom Unity fonts (which just map an image to a character). You will either need to import an actual font file (perhaps one you make yourself with a 3rd party tool), or try programming a conversion of Unity Sprite to TextMesh Pro Font.
