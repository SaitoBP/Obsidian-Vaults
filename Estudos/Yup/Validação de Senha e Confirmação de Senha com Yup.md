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

Caso ocorram erros no typescript, a seguinte solução pode servir
[Solução](https://github.com/jquense/yup/issues/1013#issuecomment-1085998986:~:text=So%20I%20found,message%20here%22).

[Referencia: StackOverflow](https://stackoverflow.com/questions/61862252/yup-schema-validation-password-and-confirmpassword-doesnt-work)