# vue-3-forms

My code following along the Vue-3-Forms course.
This code is much different from the course since I used the newer composition API.

## To run this project

### Setup

Install the necessary dependencies

```zsh
$ npm install
```

### Launch

Start the development server

```zsh
$ npm run dev
```

Launch the mockup JSON-SERVER

```zsh
$ npm run mockserver
```

## AY11N Takeaways

- Typing Form Fields

  - Do not ignore the type property when creating form fields/buttons. - They give better autocompletion for forms - They allow screen readers to properly interpret what input is expected - They allow devices to adapt and provide accesibility - Ex: `type="tel"` will make most phones show a keypad instead of keyboard
    Some Types for input elements:

- Fieldset
  -Field sets group form inputs, and have a legend element explains what is expected from the user.

|     button     | email  |  number  | search | url  |
| :------------: | :----: | :------: | :----: | :--: |
|    checkbox    |  file  | password | submit | week |
|     color      | hidden |  radio   |  tel   | date |
| datetime-local | month  |  reset   |  time  |

example:

```html
<fieldset>
  <legend>Name and describe your event</legend>
  <div class="form-item">
    <BaseInput name="title" v-model="event.title" />
  </div>
  <div class="form-item">
    <BaseInput name="description" v-model="event.description" />
  </div>
</fieldset>
```

- Labels
  - Placeholders are nice, Labels are mandatory! - Placeholders dissapear when the field is interacted with. without a label the user will have almost no feedback on the expected input - Linking labels to the inputs - Nest the input into the label tag - !Recommended: use id's -> give the label a `for="elementid'` attribute
    example:

```html
<lable for="login-form-username">Username</lable>
<input id="login-form-username" name="username" type="text" />
```

- AriaDescribed By
  Ariadescribed by takes in the ID of any html elemenbt that describes it, This way we could for example: make sure screen readers know what error message should describe what input
- - Aria-live
    With aria live we can further increase awareness, by adding ```aria-live="assertive"```,
    most screen readers will pick up on this and make sure to announce the newly shown error
- Aria-invalid
The aria invalid attribute will tell screen readers if the input field has been filled out valid,
We can also use 
  - aria-readonly
  - aria-disabled
  - aria-required
example:
```html
<fieldset>
  <legend>The computer knows the error belongs to the field!</legend>
  <label for="myUniqueIdBecauseIAmSpecial">Email</label>
  <input id="myUniqueIdBecauseIAmSpecial"
         :aria-describedby="props.error ? 'myUniqueIdBecauseIAmSpecial-error' : null"
         :aria-invalid="props.error ? true : null"
         type="email" 
         name="email" />
  <p v-if="props.error" id="myUniqueIdBecauseIAmSpecial-error" aria-live="assertive" >There was an error in the email!</p>
  >
</fieldset>
```
- Do not disable the Submit button!
Screen readers completely ignore disabled buttons.
There for it is recomended to write proper validation and provide feedback if you ever disable the button. As for screen reader users the button will just vanish in thin air