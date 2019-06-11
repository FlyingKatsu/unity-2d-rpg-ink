# Extras
This page describes additional utilities for writing Ink stories.

## Comments
Comments are lines of text that have no effect on the story. They can be used as reminders or explanations to other writers or developers.

Mark text as a comment by using two forward slashes:
`// Should we add more options to this question?`

If you know something needs to be changed later, you can mark it with a special kind of comment called a `TODO`
`TODO: add another option to this question`

Comments can also span multiple lines, by starting with `/*` and ending with `*/`:
```
/*
    ====================================================================
    This is a really long comment, but it makes my script more readable
    because I can add a bunch of extra = to act as a divider!
    ====================================================================
*/
```

## Tags
Similar to comments, tags also have no effect on the story, but they can be used to pass metadata to another game engine, such as a sound effect to play or an image to display.

Tags use hashtags, of course, and can be written either before a line of text, or in-line:
```
# sfx: crash
Oh no, I dropped the vase! # mood: stressed, prop: broken vase
```

See [Custom/Metadata](Custom.md#metadata) for a list of tags supported by our Unity scripts.
