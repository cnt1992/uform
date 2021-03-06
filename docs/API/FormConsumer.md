# FormConsumer

## 介绍

用于表单的跨组件通讯提交重置状态同步等操作，它主要与FormProvider一起使用

## 依赖

```javascript
import {FormConsumer} from '@uform/react'
```

## API

```typescript
<FormConsumer>
    {({
      status  : String<"changed" | "resetd" | "initialize" | "submitting" | "submitted">, //表单活动状态
      state   : FormState,//表单状态模型
      schema  : Object,//表单schema
      submit(),//表单提交
      reset(),//表单重置
      dispatch(name : String,payload : any)//触发effect自定义事件 
    })=>ReactElement)
</FormConsumer>
```

## 用例

```jsx
import React, { Component } from 'react'
import ReactDOM from 'react-dom'
import SchemaForm, {
  registerFormField,
  Field,  
  connect,
  FormProvider,
  FormConsumer
} from '@uform/react'

registerFormField(
  'string',
  connect()(props => <input {...props} value={props.value || ''} />)
)

ReactDOM.render(
   <FormProvider>
       <SchemaForm defaultValue={{aa:'123'}} onSubmit={values=>alert(JSON.stringify(values))}>
         <Field name="aa" type="string"/>
         <button htmlType="submit">内部提交</button>
       </SchemaForm>
       <FormConsumer>
         {({submit})=>(<button onClick={submit}>外部提交</button>)}
       </FormConsumer>
   </FormProvider>
,document.getElementById('root'))
```
