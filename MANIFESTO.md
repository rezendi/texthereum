The Texthereum Manifesto
========================

It should be easy to send small(ish) amounts of cryptocurrencies via text message.
The recipient shouldn’t need a wallet, or an app, or an account. This would expand
the group "people you can send cryptocurrency to" from the mere millions of
people, those with wallets and accounts at crypto exchanges, to _anyone with a
phone_, i.e. billions.

Then you could send cryptocurrency directly as aid, and/or to those struck by
crisis, a la [GiveDirectly](https://www.givedirectly.org/). (Yes, they'd then
have to find/use a way to convert it -- but they would still be in immediate
direct possession of aid money, which they might not even want to convert
immediately, preferring to hold it to hedge against local inflation.) You could
pay your share of a group expense in crypto, on the spot, with minimal hassle,
even if the recipient has no wallet. You could immediately send money across
borders to anyone with a phone, or construct programmatic crypto rewards which
anyone with a phone could claim. 

Others have thought this. But what do all of the existing ‘send crypto via text’
solutions demand? “Download our app / Create an account / Sign up at our site /
Use our token.” No, stop it, wrong. Nobody wants that--and it’s not necessary.
Cryptocurrencies come with everything needed to transfer value via text
_already built in_. You don’t need an account, or an app, or a site, or a token.
All you need is a protocol: a repeatable way to turn the recipient’s phone
number, and a password for security, into the private key which can access the
transferred money.

“What? Working with raw private keys? Ones built from not-entirely-random data,
therefore lower entropy? Using notoriously hackable and SIM-swappable SMS? That
is horrifically unsafe and insecure and completely unacceptable!” No, stop it,
wrong. I mean, I certainly wouldn’t send a million dollars this way. And I’d
certainly favor Signal and WhatsApp over SMS. But the threat model for a
million-dollar transaction is _very very **very** different_ from the threat
model for fifty bucks. For the latter, a protocol protected by decent
passwords is good enough.

So what is this protocol? It’s quite simple:
1. Take the recipient’s phone number.
2. Pick a password, with decent length and complexity requirements.
3. Use 1. and 2. to create an Ethereum private key in a deterministic way.
4. Use that private key to create its corresponding Ethereum address.
5. Send ether--or any ERC-20 token--to that address.
6. Text the password to the recipient's phone number.
7. Recipient goes through steps 1-3 again to get the address's private key.

You may be thinking: "This sounds super low level and complex!" Sure. That's
why I built a web service to handle steps 1 through 4 for you. That site
runs everything locally in your browser, of course, all data is ephemeral and
transient, nothing is ever stored, etc. (And again, before your head explodes,
the threat model for "occasionally sending $50 to your buddy" is very very
different from the threat model for "a crypto whale's life savings.") This
reduces the procedure to:
1. Go to [texthereum.com](https://texthereum.com), enter the recipient's phone
number, pick a password.
2. Text that password and an explanatory URL to the recipient’s phone.
(The site generates boilerplate text to copy/paste.)
3. Send ether, or ERC-20 tokens, to the generated address.
4. Recipient goes to [texthereum.com](https://texthereum.com/receive) and uses
the password they were texted to get their private key -- basically, an
"electronic paper wallet" -- to be imported (or swept) into a more
formal / secure wallet, then perhaps exchanged for fiat.

Note that you don’t have to use the web site at _all_ for any of this. It’s
just a convenience and a reference implementation. You can do it all yourself
on an air-gapped computer in an underground bunker if you really want.

Note also that there's room for higher-level services here, such as a service
to generate the password and host it (but not the money!) in a kind of password
escrow, send an initial text to ensure the number is correct by having the
recipient verify obscure/trivial knowledge shared by both parties, and only
then actually send the recipient the generated password. I expect you'll be
able to think of more yet. This protocol is (deliberately) primitive, but it's
a primitive atop which more sophisticated services could be built.

Obviously this is an alpha release and you should probably stick to testnets,
for now. Even if/when you start sending real money, don't send very much.
(If you're thinking: "gas fees make this prohibitive right now!" -- well,
there are times when that's true. But Ethereum 2.0 wsould address that.)

A few potential use cases spelled out in more detail:

1. Suppose you want **to airdrop cryptocurency** to everyone in a given region,
or with a given phone number prefix, again a la GiveDirectly. Instead of
ensuring all recipients have wallets, tracking every address, etc., you can
just transfer it all by phone and then have your agent help people handle it
via public education sessions, easily resend any messages that were
accidentally deleted, etc.

2. Suppose you land in London, go for a fancy meal with acquaintances, then
realize you don’t have any pounds on you. So you ask "**Can I pay you with
crypto?**" Instead of requiring the recipient to download a wallet, deal with a
mnemonic phrase, figure out addresses, etc., on the spot -- unrealistically
complex and obnoxious -- you just ask them for their phone number. Maybe send
them a quick confirmation text to ensure you got it right. Then just come up
with a witty password, send them a text with it, fire up your wallet, and
transfer 0.2 ETH to the address copied from [texthereum.com](https://texthereum.com). The hard part is
now the witty password.

3. Suppose you don’t even want to send money to a phone; you just want **to
reward whoever solves a puzzle first**. You do this by making its solutions
a 15-digit number and a password. Then whoever gets it first can go to
[texthereum.com/receive](https://texthereum.com/receive), enter those values,
get the private key, and claim its contents.

4. This doesn't just work for phone numbers. It could also be used for email
addresses, Twitter handles, or any other kind of unique identifier.

Of course, senders still have to perform the actual blockchain transfers
themselves. (A higher-level service _could_ do this, but of course would have
to be a registered and regulated money transmitter, in most countries.)
Texthereum can’t help with that user experience, or the recpient’s experience
once they receive their cryptocurrency.

But there are no _additional_ user experiences: no account to sign up for,
no app to download, no "utility" token to deal with, nothing else to think
about or keep track of. It’s simple ... and it’s already baked in, right at
the protocol level, waiting to be used.

You may be wondering: can you do this with Bitcoin too? And the answer is:
you sure can. The algorithms are just a little different. See the very similar
[BTextC Manifesto](https://github.com/rezendi/texthereum/blob/main/btextc/MANIFESTO.md)...

