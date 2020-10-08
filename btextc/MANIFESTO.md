The BTextC Manifesto
========================

It should be easy to send small(ish) amounts of bitcoin via text message.
The recipient shouldn’t need a wallet, or an app, or an account.

But what do all of the existing ‘send crypto via text’ solutions demand?
“Download our app / Create an account / Sign up at our site / Use our token.”
No, stop it, wrong. Nobody wants that--and it’s not necessary. Bitcoin comes
with everything needed to transfer value via text _already built in_. You don’t
need an account, or an app, or a site, or a token. All you need is a protocol:
a repeatable way to turn the recipient’s phone number, and a password for
security, into the private key which can access the transferred money.

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
3. Use 1. and 2. to create a Bitcoin private key in a deterministic way.
4. Use that private key to create its corresponding Bitcoin address.
5. Send bitcoin to that address.
6. Text the password to the recipient's phone number.
7. Recipient goes through steps 1-3 again to get the address's private key.

You may be thinking: "This sounds super low level and complex!" Sure. That's
why we built a web service to handle steps 1 through 4 for you. That site
runs everything locally in your browser, of course, all data is ephemeral and
transient, nothing is ever stored, etc. (And again, before your head explodes,
the threat model for "occasionally sending $50 to your buddy" is very very
different from the threat model for "a crypto whale's life savings.") This
reduces the procedure to:
1. Go to [BTextC.com](https://btextc.com/), enter the recipient's phone number, pick a password.
2. Text that password and an explanatory URL to the recipient’s phone.
(The site generates boilerplate text to copy/paste.)
3. Send ether, or ERC-20 tokens, to the generated address.
4. Recipient goes to [BTextC.com](https://btextc.com/receive) and uses the
password they were texted to get their private key -- basically, an
"electronic paper wallet" -- to be imported (or swept) into a more
formal / secure wallet, then perhaps exchanged for fiat.

Note that you don’t have to use the web site at _all_ for any of this. It’s
just a convenience and a reference implementation. You can do it all yourself
on an air-gapped computer in an underground bunker if you really want.

So what might this be good for? Well, my own not-so-secret long-term hope is
to eventually replace much of the world’s international development aid with
direct cash transfers to individuals, a la [GiveDirectly](https://www.givedirectly.org/). Bitcoin transfers
seem like a potential elegant solution to managing that worldwide, while also,
very possibly, helping recipients hedge against local-currency inflation.

In the interim, here are a few possibilities:

1. Suppose you want **to airdrop bitcoin** to everyone in a given region, or with
a given phone number prefix, again a la GiveDirectly. Instead of ensuring all
recipients have wallets, tracking every address, etc., you can just transfer
it all by phone and then have your agent help people handle it via public
education sessions, easily resend any accidentally deleted messages, etc.

2. Suppose you land in London, go for a fancy meal with acquaintances, then
realize you don’t have any pounds on you. So you ask "**Can I pay you with
Bitcoin?**" Instead of requiring the recipient to download a wallet, deal with a
mnemonic phrase, figure out addresses, etc., on the spot -- unrealistically
complex and obnoxious -- you just ask them for their phone number. Maybe send
them a quick confirmation text to ensure you got it right. Then just come up
with a witty password, send them a text with it, fire up your wallet, and
transfer 0.2 ETH to the address copied from [BTextC.com](https://btextc.com/).
The hard part is now the witty password.

3. Suppose you don’t even want to send bitcoin to a phone; you just want **to
reward whoever solves a puzzle first**. You do this by making its solutions
a 15-digit number and a password. Then whoever gets it first can go to
[BTextC.com/receive](https://btextc.com/receive), enter those values, get the
private key, and claim its contents. Think about it a while and I bet you’ll
come up with some other non-phone use cases too...

Of course, you still have to perform the actual blockchain transfers yourself.
BTextC can’t help with that user experience, or the recpient’s experience
once they receive their cryptocurrency. But there are no _additional_ user
experiences: no account to sign up for, no app to download, nothing else to
think about or keep track of. It’s simple ... and it’s already baked in, right
at the protocol level, waiting to be used.

You may be wondering: can you do this with Ethereum too? And the answer is:
you sure can. See the very similar
[Texthereum Manifesto](https://github.com/rezendi/texthereum/blob/main/MANIFESTO.md)...
