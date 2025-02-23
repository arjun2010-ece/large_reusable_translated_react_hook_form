# Live demo here:: https://checkout-form-rhf.web.app/

# LARGE TRANSLATED REUSABLE REACT HOOK FORM EXAMPLE.

Features::
We can reuse the form "AddressForm" multiple times like below::

`<AddressForm title={t('text.shippingAddress')} parentName="shippingAddress" />`

and

`
<AddressForm title={t('text.personalAddress')} parentName="personalAddress" />
`

Here with different parentName props the fields ecome different and thus reusable too.

Way to use it:::

1. Use FormProvider and form tag only in the root of the project then break down each form into sub components and fetch all things like register, errors in different forms by useFormContext.

useForm() hook is always used onetime for one form tag.

```

const methods = useForm<Order>({
        mode: 'onBlur',
        defaultValues: order,
        resolver: yupResolver(schema), // may or may not be used
    });
    
    
 <FormProvider {...methods}>
            <form onSubmit={methods.handleSubmit(onSubmit)}>
                <ContactInfoForm />
                <hr className="mt-4 mb3" />

                <AddressForm
                    title={t('text.shippingAddress')}
                    parentName="shippingAddress"
                />
                <hr className="mt-4 mb3" />

                <ShippingOptionsForm
                    onShippingMethodChanged={onShippingMethodChanged}
                />
                <hr className="mt-4 mb3" />

                <PaymentForm />

                <AddressForm
                    title={t('text.officeAddress')}
                    parentName="officeAddress"
                />

                <CheckoutActions
                    orderTotal={Order.getOrderTotal(order).orderTotal}
                />
            </form>
        </FormProvider>
```

And then in ContactInfoForm e.g::

`
import { useFormContext } from 'react-hook-form';

const { errors, register } = useFormContext();
`

same in AddressForm e.g::

`
import { useFormContext } from 'react-hook-form';

const { errors, register } = useFormContext();
`

and so on
