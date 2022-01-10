---
title: Jekyll 설치방법
category: Git
order: 1
---

1. **[RubyInstaller](https://rubyinstaller.org/downloads/)**에서 devkit_64로 오른쪽에서 추천하는 2.7버전 설치함 (devkit깔면 Gems 따로 설치 안해도됨)
2. 윈도우에 Start Command Prompt with Ruby 클릭 `ruby -v` 잘깔렸는지 체크
3. `gem install jekyll bundler`
4. `gem install bundler`
5. `bundler install` 하니 안되서 설치하라는 데로 `gem install bundler:1.16.4` 함
6. `bundler install` 다시 하고 `bundle exec jekyll serve` 했는데 안됨
7. `bundler updata`
8. **Window 버전 주의사항** `gem install tzinfo / gem install tzinfo-data` 설치 후
9. Gemfile에 추가

   > gem 'tzinfo'

   > gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw, :jruby]

10. `bundle exec jekyll serve` 하면 정상 작동함 + 수정할때마다 실행해줘야 함.
