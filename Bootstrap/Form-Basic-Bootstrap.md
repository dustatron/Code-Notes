# Basic Input Form

[Documentation](https://react-bootstrap.github.io/components/forms/)

![Screen Shot ](/Users/dusty/Documents/Typora/React/Bootstrap/img/Screen Shot 2020-05-12 at 5.25.14 PM.png)

```javascript
<Form>
  <Form.Group controlId="formBasicEmail">
    <Form.Label>Email address</Form.Label>
    <Form.Control type="email" placeholder="Enter email" />
    <Form.Text className="text-muted">
      We'll never share your email with anyone else.
    </Form.Text>
  </Form.Group>

  <Form.Group controlId="formBasicPassword">
    <Form.Label>Password</Form.Label>
    <Form.Control type="password" placeholder="Password" />
  </Form.Group>
  <Form.Group controlId="formBasicCheckbox">
    <Form.Check type="checkbox" label="Check me out" />
  </Form.Group>
  <Button variant="primary" type="submit">
    Submit
  </Button>
</Form>
```



## Select 

```javascript
<Form>
  <Form.Group controlId="exampleForm.SelectCustom">
    <Form.Label>Custom select</Form.Label>
    <Form.Control as="select" custom>
      <option>1</option>
      <option>2</option>
      <option>3</option>
      <option>4</option>
      <option>5</option>
    </Form.Control>
  </Form.Group>
</Form>
```

