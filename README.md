# hello_meleu

A useless gem created for the sole purpose to show people how to create a
Ruby Gem and publish it to <https://RubyGems.org>.

In this README I describe 3 simple steps to create a Ruby Gem.

**IMPORTANT**: if you want to follow along and create your own gem you'll
need to use a different name than `hello_meleu`!

## Table of Contents

- [Step 1: very minimum files you need for a gem](#step-1-very-minimum-files-you-need-for-a-gem)
- [Step 2: add metadata with useful links](#step-2-add-metadata-with-useful-links)
- [Step 3: add documentation](#step-3-add-documentation)
- [Final Words](#final-words)

## Step 1: very minimum files you need for a gem

The very minimum you need to create a Ruby Gem and publish it to RubyGems.org
is a file structure like this:

```
hello_meleu/
├── hello_meleu.gemspec
└── lib
    └── hello_meleu.rb
```

The `lib/hello_meleu.rb` is as simple as this:

```ruby
class HelloMeleu
  def self.hello
    'Hello meleu!'
  end
end
```

The very minimum you need for your `.gemspec` is something like this:

```ruby
Gem::Specification.new do |s|
  s.name = 'hello_meleu'
  s.authors = ['meleu']
  s.files = ['lib/hello_meleu.rb']
  s.summary = 'Greeting meleu'
  s.version = '0.0.1'
end
```

The most important field here is the `s.files`, as this is an array with the
name of the source file(s) we want to distribute in our gem. In our case here
it's just one file, then we have an array with only one string: `["lib/hello_meleu.rb"]`.

In the [official documenation](https://guides.rubygems.org/specification-reference/)
you can see the details of all these fields. Another reading that I found
enlightening was [this article by Piotr Murach](https://piotrmurach.com/articles/writing-a-ruby-gem-specification/).

These two files (the .rb code and the gemspec) are enough to build and publish our gem!

```bash
# building your gem
gem build hello_meleu.gemspec
# this creates the hello_meleu-0.0.1.gem file

# publish your gem to RubyGems.org
gem push hello_meleu-0.0.1.gem
# in the first run it'll give you instructions
# to create a RubyGems.org account
```

🎉 Yay! We published our gem at <https://rubygems.org/gems/hello_meleu>.

Now you can even install it:
```bash
gem install hello_meleu

# now launch irb, require 'hello_meleu'
# and execute `HelloMeleu.hello`
```

- [Link to the commit](https://github.com/meleu/hello_meleu/commit/7a729ce81030d00dfc6addbff456c39b11c4ffc0).
    - NOTE: in this first commit I also created a `.gitignore` file (it's not needed
for a Ruby Gem, but useful when working with git repositories). The file was
created via <https://gitignore.io>.


## Step 2: add metadata with useful links

We want our gem to be open source, right! We want to share the code to the
world and hopefully receive contributions from the community.

A cool thing to do is to add a link to the project's repo in our
[gem's page at RubyGems.org](https://rubygems.org/gems/hello_meleu).

So, let's enrich our `hello_meleu.gemspec` with the following content:

```ruby
Gem::Specification.new do |s|
  # ...
  s.version = '0.0.2'

  s.homepage = 'https://github.com/meleu/hello_meleu'
  s.metadata = {
    'bug_tracker_uri' => "#{s.homepage}/issues",
    'changelog_uri' => "#{s.homepage}/releases",
    'wiki_uri' => "#{s.homepage}/wiki",
    'source_code_uri' => s.homepage,
  }
end
```

You can see that I specified the homepage of the gem as the github repository,
and then added some other useful links to report bugs, check release notes, wiki, etc.

Have you noticed that I bumped the version to `0.0.2`? Although we didn't change
anything in our gem's logic, we need to bump the version. This is needed because
once we publish a specific version, we cannot change it anymore!

Once we added those links to our `gemspec`, let's publish our gem again:

```bash
# build the gem
gem build hello_meleu.gemspec

# publish a new version
gem push hello_meleu-0.0.2.gem
```

Now go the [gem's page](https://rubygems.org/gems/hello_meleu) and check those
links the right sidebar! That's cool, isn't it? :)

- [Link to the commit](https://github.com/meleu/hello_meleu/commit/514fdf81da5995caf8c2e1d1ee17c1a2eeff668c)


## Step 3: add documentation

A nice practice developers have is to document their libraries so other
developers can know how to use them. Here we are going to document our
code adding *top-level documentation comments*. Like this:

```ruby
# Class used to greet meleu with "hello".
class HelloMeleu
  # Greets meleu with "hello".
  #
  # @return [String] "Hello meleu!"
  def self.hello
    'Hello meleu!'
  end
end
```

You may be thinking: will other developers using my gem really open each source
file and read these comments?!

Yeah... probably not...

But there's a cool thing that RubyGems.org does for us...

Let's add the `documentation_uri` to our gem's metadata:

```ruby
Gem::Specification.new do |s|
  # ...
  s.version = '0.0.3'

  s.metadata = {
    # ...
    'documentation_uri' => 'https://www.rubydoc.info/gems/hello_meleu'
  }
end
```

The link in `documentation_uri` is a cool service provided by RubGems.org,
where it automatically create a documentation site for our gem. And yeah!
The service read the top-level documentation comments in our code and our
gem will have a neat documentation website!

Let's publish a new version and check it:

```bash
# build the gem
gem build hello_meleu.gemspec

# publish a new version
gem push hello_meleu-0.0.3.gem
```

Now go the [gem's page](https://rubygems.org/gems/hello_meleu) and look for the
**Documentation** link in that right sidebar. Click on it and you'll see the
[documentation website you have for your gem](https://www.rubydoc.info/gems/hello_meleu/0.0.10).
Note that your comments are there, documenting your class and method.

- [Link to the commit](https://github.com/meleu/hello_meleu/commit/da23a9cad0a3906a54b3df6d1208f63d37398193)

---

## Final Words

Of course there are more to say about maintaining a Ruby Gem, but I hope you now
can see that it's really easy to get started! :)

Happy coding!
