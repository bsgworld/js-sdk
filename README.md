# @bsgworld/js-sdk

BSG JavaScript/TypeScript SDK for One-API.

## Installation

```bash
npm install @bsgworld/js-sdk
# or
yarn add @bsgworld/js-sdk
```

### Requirements

- Node.js 16 or later
- TypeScript 4.7+ (for TypeScript projects)

## Getting Started

```typescript
import { Configuration, AuthApi, CampaignSMSApi } from '@bsgworld/js-sdk';

// 1. Authenticate - get JWT token
const authApi = new AuthApi();

const loginResponse = await authApi.login({
    api_key: 'live_XXXXXXXXXXXXXXXXXXXX'
});

const token = loginResponse.data.bearer;

// 2. Configure client with JWT token
const config = new Configuration({
    basePath: 'https://one-api.bsg.world',
    accessToken: token
});

// 3. Send SMS
const smsApi = new CampaignSMSApi(config);

const smsResponse = await smsApi.smsSend({
    phones: new Set([{ number: 380661234567 }]),
    sender: 'BSG',
    text: 'Hello from BSG!'
});

console.log('Campaign ID:', smsResponse.data.id);
```

### CommonJS Usage

```javascript
const { Configuration, AuthApi, CampaignSMSApi } = require('@bsgworld/js-sdk');

async function sendSms() {
    // 1. Get JWT token
    const authApi = new AuthApi();
    const loginResponse = await authApi.login({
        api_key: 'live_XXXXXXXXXXXXXXXXXXXX'
    });

    // 2. Configure with token
    const config = new Configuration({
        basePath: 'https://one-api.bsg.world',
        accessToken: loginResponse.data.bearer
    });

    // 3. Send SMS
    const smsApi = new CampaignSMSApi(config);
    const response = await smsApi.smsSend({
        phones: new Set([{ number: 380661234567 }]),
        sender: 'BSG',
        text: 'Hello from BSG!'
    });

    console.log('Campaign ID:', response.data.id);
}

sendSms().catch(console.error);
```

## API Reference

Documentation is available locally in the `docs/` folder (generated with [TypeDoc](https://typedoc.org/)).

To regenerate documentation:

```bash
npm run docs
```

### Available API Classes

| Class | Description |
| ----- | ----------- |
| `AuthApi` | Authentication - login, token refresh |
| `BalanceApi` | Account balance and tariffs |
| `CampaignSMSApi` | Send SMS campaigns |
| `CampaignRCSApi` | Send RCS messages |
| `CampaignWhatsAppApi` | Send WhatsApp messages |
| `ContactApi` | Manage contacts |
| `ContactListApi` | Manage contact lists |
| `SendersApi` | Manage sender names |
| `TwoFAOTPApi` | Two-factor authentication (OTP) |
| `ShortLinksApi` | URL shortener |

### All Endpoints

All URIs are relative to *https://one-api.bsg.world*

| Class | Method | HTTP request | Description |
| ----- | ------ | ------------ | ----------- |
| `AccountSettingsApi` | `getSettingsAddressBookFieldsById` | **GET** /api/settings/address-book-fields/{id} | Get settings value |
| `AuthApi` | `login` | **POST** /api/auth/login | Receive JWT token |
| `AuthApi` | `refreshToken` | **POST** /api/auth/refresh | Refresh JWT token |
| `BalanceApi` | `accountBalance` | **GET** /api/accounts/balance | Get balance |
| `BalanceApi` | `accountTariffs` | **GET** /api/accounts/tariff | Get tariffs |
| `CampaignApi` | `campaign` | **GET** /api/campaigns/{id} | Get campaign info |
| `CampaignApi` | `campaignDetails` | **GET** /api/campaigns/{id}/detail | Get campaign details |
| `CampaignApi` | `campaignPrice` | **POST** /api/campaigns/price | Calculate campaign price |
| `CampaignApi` | `campaignStop` | **PATCH** /api/campaigns/{id}/stop | Cancel campaign |
| `CampaignApi` | `campaigns` | **GET** /api/campaigns | List of campaigns |
| `CampaignRCSApi` | `rcsSend` | **POST** /api/campaigns/rcs/send | Send RCS message |
| `CampaignRCSApi` | `rcsSendGroups` | **POST** /api/campaigns/rcs/send-groups | Send RCS message to contact list |
| `CampaignRCSApi` | `rcsSingle` | **POST** /api/messages/rcs/send | Send single RCS message |
| `CampaignSMSApi` | `smsSend` | **POST** /api/campaigns/sms/send | Send SMS campaign |
| `CampaignSMSApi` | `smsSendGroups` | **POST** /api/campaigns/sms/send-groups | Send SMS to contact list |
| `CampaignSMSApi` | `smsSendIndividual` | **POST** /api/campaigns/sms/send-individual | Send SMS with different text |
| `CampaignWhatsAppApi` | `postCampaignsWhatsappSend` | **POST** /api/campaigns/whatsapp/send | Send WhatsApp campaign |
| `ContactApi` | `contact` | **GET** /api/contacts/{id} | Get contact by ID |
| `ContactApi` | `contactCreate` | **POST** /api/contacts | Create a contact |
| `ContactApi` | `contactDelete` | **DELETE** /api/contacts/{id} | Delete contact |
| `ContactApi` | `contactUpdate` | **PUT** /api/contacts/{id} | Update contact |
| `ContactApi` | `contacts` | **GET** /api/contacts | List of contacts |
| `ContactApi` | `contactsDelete` | **POST** /api/contacts/delete | Delete multiple contacts |
| `ContactApi` | `contactsSearch` | **GET** /api/contacts/search | Search contacts |
| `ContactFieldApi` | `contactFieldCreate` | **POST** /api/contacts/fields | Create contact field |
| `ContactFieldApi` | `contactFieldUpdate` | **PATCH** /api/contacts/fields/{id} | Update contact field |
| `ContactFieldApi` | `contactFields` | **GET** /api/contacts/fields | List of contact fields |
| `ContactFieldApi` | `postContactsFieldsDelete` | **POST** /api/contacts/fields/delete | Delete contact fields by ids |
| `ContactListApi` | `contactList` | **GET** /api/groups/{id} | Get list by id |
| `ContactListApi` | `contactListAttach` | **POST** /api/groups/attach | Add contacts to the list |
| `ContactListApi` | `contactListCreate` | **POST** /api/groups | Create list |
| `ContactListApi` | `contactListDelete` | **DELETE** /api/groups/{id} | Delete list |
| `ContactListApi` | `contactListDetach` | **POST** /api/groups/detach | Remove contacts from the list |
| `ContactListApi` | `contactListSearch` | **GET** /api/groups/search | Search list |
| `ContactListApi` | `contactListUpdate` | **PUT** /api/groups/{id} | Update list |
| `ContactListApi` | `contactLists` | **GET** /api/groups | List of contact lists |
| `EmailApi` | `emailSend` | **POST** /api/email/send-emails | Send Email |
| `EmailApi` | `emailTemplateSend` | **POST** /api/email/send-template-emails | Send Email template |
| `InternalCorePriceApi` | `getInternalCorePrices` | **GET** /api/internal/core/prices | Get price list for each country |
| `InternalCorePriceApi` | `getInternalCorePricesByCountryCode` | **GET** /api/internal/core/prices/{countryCode} | Get prices for country |
| `InternalCountryApi` | `getInternalCountries` | **GET** /api/internal/countries | Get countries list |
| `InternalCurrencyApi` | `getInternalCurrencies` | **GET** /api/internal/currencies | Get currencies list  |
| `InternalTwoFAApi` | `getInternal2faAuthenticationsFullPrice` | **GET** /api/internal/2fa/authentications/full-price | Show TwoFA authentication full price |
| `InternalWstPriceApi` | `getInternalWstPrices` | **GET** /api/internal/wst/prices | Get price list for each country |
| `InternalWstPriceApi` | `getInternalWstPricesByCountryCode` | **GET** /api/internal/wst/prices/{countryCode} | Get prices for country |
| `MessagesSMSApi` | `getMessages` | **GET** /api/messages | Find messages |
| `MessagesWhatsAppApi` | `whatsappSingle` | **POST** /api/messages/whatsapp/send | Send single WhatsApp message |
| `SendersApi` | `senderRequestLegal` | **POST** /api/senders/requests/legal | Sender registration by a legal entity |
| `SendersApi` | `senderRequestNatural` | **POST** /api/senders/requests/natural | Sender registration by an individual |
| `SendersApi` | `senderRequests` | **GET** /api/senders/requests/sms | List of Sender Requests |
| `SendersApi` | `senders` | **GET** /api/senders | List of Senders |
| `ShortDomainsApi` | `shortUrlsDomain` | **GET** /api/short-url/domains/{uuid} | Get domain by uuid |
| `ShortDomainsApi` | `shortUrlsDomainCreate` | **POST** /api/short-url/domains | Add domain |
| `ShortDomainsApi` | `shortUrlsDomainRemove` | **DELETE** /api/short-url/domains/{uuid} | Remove domain |
| `ShortDomainsApi` | `shortUrlsDomainUpdate` | **PUT** /api/short-url/domains/{uuid} | Update domain |
| `ShortDomainsApi` | `shortUrlsDomains` | **GET** /api/short-url/domains | List of domains |
| `ShortLinksApi` | `shortUrlsClicks` | **GET** /api/short-url/clicks | List of clicks |
| `ShortLinksApi` | `shortUrlsLink` | **GET** /api/short-url/links/{uuid}/statistics | Get short link statistic |
| `ShortLinksApi` | `shortUrlsLinkCreate` | **POST** /api/short-url/links | Create short link |
| `ShortLinksApi` | `shortUrlsLinkDelete` | **DELETE** /api/short-url/links/{uuid} | Remove short link |
| `ShortLinksApi` | `shortUrlsLinkUpdate` | **PUT** /api/short-url/links/{uuid} | Update short link |
| `ShortLinksApi` | `shortUrlsLinks` | **GET** /api/short-url/links | List of short links |
| `StopListApi` | `stoplistAdd` | **POST** /api/stoplist/attach | Add contacts to stop list |
| `StopListApi` | `stoplistItems` | **GET** /api/stoplist | List the contacts of stop lists |
| `StopListApi` | `stoplistRemove` | **POST** /api/stoplist/detach | Remove contacts from stop list |
| `StopListApi` | `stoplistSearch` | **GET** /api/stoplist/search | Search contacts in Stop lists |
| `TwoFAOTPApi` | `cancelOtp` | **POST** /api/2fa/authentications/{id}/cancel | Cancel the authentication session |
| `TwoFAOTPApi` | `otpList` | **GET** /api/2fa/authentications | List of authentication sessions |
| `TwoFAOTPApi` | `resendOtp` | **POST** /api/2fa/authentications/otp/{id}/resend | Resend the one-time code |
| `TwoFAOTPApi` | `sendOtp` | **POST** /api/2fa/authentications/otp | Send One-time password |
| `TwoFAOTPApi` | `statusOtp` | **GET** /api/2fa/authentications/{id} | Check authentication status |
| `TwoFAOTPApi` | `verifyOtp` | **POST** /api/2fa/authentications/otp/{id}/verify | Check one-time Code |
| `TwoFATemplatesApi` | `otpTemplate` | **GET** /api/2fa/authentications/templates/{templateId} | Get message template |
| `TwoFATemplatesApi` | `otpTemplateCreate` | **POST** /api/2fa/authentications/templates | Create a message template |
| `TwoFATemplatesApi` | `otpTemplateDelete` | **DELETE** /api/2fa/authentications/templates/{templateId} | Delete a message template |
| `TwoFATemplatesApi` | `otpTemplateList` | **GET** /api/2fa/authentications/templates | List of message templates |


## Authorization

All API calls (except `AuthApi.login`) require JWT Bearer token authentication.

```typescript
const config = new Configuration({
    basePath: 'https://one-api.bsg.world',
    accessToken: 'your-jwt-token'
});
```

## Documentation

- [BSG API Documentation](https://bsg.world/developers)
- [Support](mailto:support@bsg.world)

## License

MIT
