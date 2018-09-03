title: "my first blog"
date: 2018-09-03
categories:
  - Jack Deng
tags:
  - test
  - highlight code
thumbnailImagePosition: right
thumbnailImage: //d1u9biwaxjngwg.cloudfront.net/highlighted-code-showcase/peak-140.jpg

# Python

{{< codeblock "archives.py" "python" "http://underscorejs.org/#compact" "archives.py" >}}
@requires_authorization
def somefunc(param1='', param2=0):
    r'''A docstring'''
    if param1 > param2: # interesting
        print 'Gre\'ater'
    return (param2 - param1 + 1 + 0b10l) or None

class SomeClass:
    pass

>>> message = '''interpreter
... prompt'''
{{< /codeblock >}}
