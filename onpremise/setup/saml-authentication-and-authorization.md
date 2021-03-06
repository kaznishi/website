# SAML Authentication and Authorization

## Authentication

Add to your `.env` file `REDASH_SAML_METADATA_URL` config value which needs to point to the SAML provider metadata url, eg `https://app.onelogin.com/saml/metadata/`. If you don’t want to communicate with IdP server to fetch a metadata, put a metadata file to the redash server as a local file, and add `REDASH_SAML_LOCAL_METADATA_PATH` instead of `REDASH_SAML_METADATA_URL`, eg `/opt/redash/metadata.xml`.

And an optional `REDASH_SAML_CALLBACK_SERVER_NAME` which contains the server name of the Redash server for the callbacks from the SAML provider (eg demo.redash.io).

And if you want to specify nameid format, add `REDASH_SAML_NAMEID_FORMAT` config value, eg `urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified`
(default is: `urn:oasis:names:tc:SAML:2.0:nameid-format:transient`).

If you want to specify entityid in `AuthnRequest`, add `REDASH_SAML_ENTITY_ID` config value, eg `http://demo.redash.io/saml/callback`.

On the SAML provider side, example configuration for OneLogin is:

SAML Consumer URL: `http://demo.redash.io/saml/login`
SAML Audience: `http://demo.redash.io/saml/callback`
SAML Recipient: `http://demo.redash.io/saml/callback`

## Okta  Example

* Single Sign On URL: `http://demo.redash.io/saml/callback`
* Recipient URL: `http://demo.redash.io/saml/callback`
* Destination URL: `http://demo.redash.io/saml/callback`
* The `FirstName` and `LastName` parameters configured to be included in the SAML assertion.

![alt text](https://raw.githubusercontent.com/yershalom/website/master/assets/screenshots/Redash_okta_settings.png "Example Okta Settings")

## Authorization

To manage group assignments in Redash using your SAML provider, configure SAML response to include attribute with key `RedashGroups`, and value as names of groups in Redash.

If you use Okta, in the `Group Attribute Statements` add `Name: RedashGroups` and `Filter: Starts with: this-is-a-group-in-redash`.
