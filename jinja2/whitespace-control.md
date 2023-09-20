# Whitespace control

Template:

```
Here are the cards for board:
{% for card in cards %}
- [{{ card.name }}]({{ card.url }}) — {{ card.age }}
{% endfor %}
```

Outcome:

```text
Here are the cards for board:

- [Tommaso: libro di religione?](https://trello.com/c/3LQ2CPbo/45-tommaso-libro-di-religione) — 3 days

- [Migrare da Dropbox a Google Drive](https://trello.com/c/Hgwv6aZ2/47-migrare-da-dropbox-a-google-drive) — 3 days

- [Buy Jason Kottke t-shirt?](https://trello.com/c/kyBTdmU4/48-buy-jason-kottke-t-shirt) — 0 days

```

Template:

```jinja2
Here are the cards for board:
{% for card in cards -%}
- [{{ card.name }}]({{ card.url }}) — {{ card.age }}
{% endfor %}
```

Outcome:

```text
Here are the cards for board:
- [Tommaso: libro di religione?](https://trello.com/c/3LQ2CPbo/45-tommaso-libro-di-religione) — 3 days
- [Migrare da Dropbox a Google Drive](https://trello.com/c/Hgwv6aZ2/47-migrare-da-dropbox-a-google-drive) — 3 days
- [Buy Jason Kottke t-shirt?](https://trello.com/c/kyBTdmU4/48-buy-jason-kottke-t-shirt) — 0 days
```

https://jinja.palletsprojects.com/en/3.1.x/templates/#whitespace-control
