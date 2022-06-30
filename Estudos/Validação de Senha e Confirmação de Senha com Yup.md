---
tags:
- Yup
---

# Validação de Senha e Confirmação de Senha com Yup
```javascript
import * as Yup from 'yup';

validationSchema: Yup.object({
  password: Yup.string().required('Password is required'),
  passwordConfirmation: Yup.string()
     .oneOf([Yup.ref('password'), null], 'Passwords must match')
});
```

Ou

```javascript
Yup.object({
  password: Yup.string().required('Password is required'),
  passwordConfirmation: Yup.string()
    .test('passwords-match', 'Passwords must match', function(value){
      return this.parent.password === value
    })
})
```
[Referencia: StackOverflow](https://stackoverflow.com/questions/61862252/yup-schema-validation-password-and-confirmpassword-doesnt-work)