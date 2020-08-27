# Email.js

**[Documentation](https://www.emailjs.com/docs/examples/reactjs/)**



## install the component

```
npm install emailjs-com
```



## set variables to template variables

```javascript
Hello {{to_name}},

You got a new message from {{from_name}}:

{{{message_html}}}

 
Best wishes,
EmailJS team
```



### build a fetch PUT request

```java
export function button1_click(event, $w) {
  // Change all values to your own
  let params = {
      user_id: 'YOUR_USER_ID',
      service_id: 'YOUR_SERVICE_ID',
      template_id: 'YOUR_TEMPLATE_ID',
      template_params: {
        'YOUR_PARAM1_NAME': 'YOUR_PARAM1_VALUE',
        'YOUR_PARAM2_NAME': 'YOUR_PARAM2_VALUE'
      }
  };

  let headers = {
      'Content-type': 'application/json'
  };

  let options = {
      method: 'POST',
      headers: headers,
      body: JSON.stringify(params)
  };

  fetch('https://api.emailjs.com/api/v1.0/email/send', options)
    .then((httpResponse) => {
        if (httpResponse.ok) {
            console.log('Your mail is sent!');
        } else {
            return httpResponse.text()
              .then(text => Promise.reject(text));
        }
    })
    .catch((error) => {
        console.log('Oops... ' + error);
    });
}
```

