# Layouts

## columns and row

[Document for Grid System](https://react-bootstrap.github.io/layout/grid/)

```javascript
<Container>  
	<Row>
    <Col sm={8}>sm=8</Col>
    <Col sm={4}>sm=4</Col>
		<Col md={{ span: 4, offset: 4 }}>{`md={{ span: 4, offset: 4 }}`}</Col>
  </Row>
</Container>
```

