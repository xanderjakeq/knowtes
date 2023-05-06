---
title: "react forms"
enableToc: false
date: "2023-05-05"
lastmod: :git
tags:
- web
---

Setting up forms in react with validation.

packages:
- [react-router](https://reactrouter.com/en/main/start/tutorial) using [createBrowserRouter](https://reactrouter.com/en/main/routers/create-browser-router)
- [[dev_notes/zod|zod]]
- [react-hook-form](https://react-hook-form.com/)
- [@hookform/resolvers](https://www.npmjs.com/package/@hookform/resolvers)

I like to [[misc/keep things simple|keep things simple]]. This way of doing things is a bit more complex than I
would like. This could be done with html form and zod, but this is more robust I 
guess.

[source](https://github.com/projectcollection/shwag)
```tsx
...
// main.tsx
const router = createBrowserRouter([
    {
        path: '/',
        element: <App />,
        errorElement: <ErrorPage />,
        children: [
			...,
            {
                path: '/forgotPassword',
                action: forgotPasswordAction,
                element: <ForgotPassword/>
            },
			...
        ]
    },
]);

...
```
The action prop, is called when the the `react-router-dom`'s `<Form/>` component is
within the route's `element` is submitted with the `method='POST'` and 
`action='/path'`. `method='GET'` will not trigger the action, but will append form inputs
to the url.

```tsx
...

// 1.
export async function forgotPasswordAction({ request }: ActionFunctionArgs) {
    const userInput = Object.fromEntries(
        (await request.formData()).entries()
    ) as ForgotPasswordParams;

    try {
		// 4.
        const res = await store.dispatch(authApi.endpoints.forgotPassword.initiate(userInput.email));

        if ('data' in res && res.data.status === 'success') {
            return redirect('/resetPassword/replace_with_reset_token');
        } else {
            alert('fail');
        }

        return null;
    } catch (e) {
        throw new Error((e as Error).message);
    }
}

export default function ForgotPassword() {
	// 2.
    const {
        register,
        handleSubmit,
        formState: { errors }
    } = useForm<ForgotPasswordParams>({
        resolver: zodResolver(LoginParamsSchema.pick({ email: true }))
    });
    const submit = useSubmit();

    const onSubmit: SubmitHandler<ForgotPasswordParams> = (data) => {
		// 3.
        submit(data, {
            method: 'post',
            action: `/forgotPassword`
        })
    }

    return (
		<Form onSubmit={handleSubmit(onSubmit)}>
			<p>
				<span>email</span>
				<input
					{...register("email")}
				/>
				{errors.email?.message}
			</p>
			<p>
				<button type="submit">get reset token</button>
			</p>
		</Form>
    )
}

...
```
`1.` the action for the route is defined. `2.` We get the methods from 
`react-hook-form`'s `useForm` hook. The resolver is what will do the validation for the
form using the zod schema. In this case the schema only have `email` defined  and is
picked from `LoginParamsSchema`. `3.` Call `submit(data, opts)` will trigger the action
for the path `action` points to. The function wrapping submit will only be called when
the user form inputs pass `handleSubmit`'s validation.

`4.` [[dev_notes/rtk-q createApi|rtk-q api endpoint]] called from [[dev_notes/call createApi endpoints outside react components|outside a react component]].