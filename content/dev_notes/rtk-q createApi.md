---
title: "rtk-q createApi"
enableToc: false
date: "2023-05-05"
lastmod: :git
tags:
- web
---

[docs](https://redux-toolkit.js.org/rtk-query/usage-with-typescript#createapi)

One of [[dev_notes/rtk query|rtk query]]'s api that help with keeping code that interact
with an backend api with a common `baseUrl`.

[source](https://github.com/projectcollection/shwag/blob/main/src/redux/services/auth.ts)
```ts
export const authApi = createApi({
    reducerPath: 'authApi',
    baseQuery: fetchBaseQuery({
        baseUrl: `${BASE_URL}/api/auth/`,
        credentials: 'include'
    }),
    endpoints: (builder) => ({
        signUpUser: builder.mutation<ResponseType, QueryParamType>({
            query: (data) => ({
                url: 'register',
                method: 'POST',
                body: data
            }),
        }),
        logoutUser: builder.query<ResponseType, QueryParamType>({
            query: () => `logout`,
        }),
        refresh: builder.query<ResponseType, QueryParamType>({
            query: () => ({
                url: 'refresh',
                method: 'GET',
            }),
        }),
        resetPassword: builder.mutation<ResponseType, QueryParamType>({
            query: ({ resetToken, password }) => ({
                url: `/resetpassword/${resetToken}`,
                method: 'PATCH',
                body: {
                    password
                }
            }),
        }),
    }),
})
```
The `endpoints` property is where to define interactions with the backend api.
`queries` are `GET` requests and doesn't take a `body` attribute, unlike `mutation` which
corresponds to writes to possible writes to the database like `POST` and `PATCH`.

```ts
export const {
    useSignUpUserMutation,
    useLogoutUserQuery,
    useResetPasswordMutation
} = authApi;
```
`createApi` generates hooks for the endpoints making it easier to get the state and 
data from the responses from within react components. Sometimes, it's necessary
to call these [[dev_notes/call createApi endpoints outside react components|endpoints outside react components]]
such is the case [[dev_notes/react forms|here]](`4.`)

