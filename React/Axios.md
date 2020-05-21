# Axios

```shell
npm install axios --save
```



### Import

```javascript
import axios from 'axios';
```

### Call

```javascript
  componentDidMount() {
    axios.get(`https://jsonplaceholder.typicode.com/users`)
      .then(res => {
        const persons = res.data;
        this.setState({ persons });
      })
  }
```

