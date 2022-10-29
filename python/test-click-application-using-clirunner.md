# How the CliRunner terminal size affects the Rich library output

The [Click](https://click.palletsprojects.com/) library has a great support for testing CLI execution. For example, you can use the CliRunner to test your CLI with something like this:

```python
from click.testing import CliRunner
from hello import hello

def test_hello_world():
  runner = CliRunner()
  result = runner.invoke(hello, ['Peter'])
  assert result.exit_code == 0
  assert result.output == 'Hello Peter!\n'
```

Everything goes as expected until you use the amazing [Rich library](https://github.com/Textualize/rich) to build some tabular output.

The CliRunner uses a terminal size of `80`, and the Rich library wraps the column content accordingly.

For example, here's the output from running the same command from my laptop's terminal (termimal size `180`):

```shell
$ rfrb it iphones --name '12 Pro Max'
                                       Refurbished Products

  Previous   Current   Saving       Name
 ────────────────────────────────────────────────────────────────────────────────────────────────
  1,309      1,109     15% (-200)   iPhone 12 Pro Max 256GB ricondizionato - Oro (Senza SIM)
  1,539      1,309     15% (-230)   iPhone 12 Pro Max 512GB ricondizionato - Oro (Senza SIM)
  1,539      1,309     15% (-230)   iPhone 12 Pro Max 512GB ricondizionato - Argento (Senza SIM)

```

And from the CliRunner (terminal size `80`):

```text
                              Refurbished Products

  Previous   Current   Saving       Name
 ──────────────────────────────────────────────────────────────────────────────
  1,309      1,109     15% (-200)   iPhone 12 Pro Max 256GB ricondizionato -
                                    Oro (Senza SIM)
  1,539      1,309     15% (-230)   iPhone 12 Pro Max 512GB ricondizionato -
                                    Oro (Senza SIM)
  1,539      1,309     15% (-230)   iPhone 12 Pro Max 512GB ricondizionato -
                                    Argento (Senza SIM)

```

So, when you are testing Rich output using the CliRunner keep in mind how ots terminal size will influence Rich's output.
