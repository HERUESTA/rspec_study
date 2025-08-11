## 環境構築方法
Dockerでの環境構築コマンドになります。
詳しいコマンドの意味とかは省略しています。
もしコマンドの意味等、気になる方いたら聞いていただけたら、お答えいたします
### Dockerの環境構築
```
docker compose build --no-cache
docker compose run --rm web gem install rails
docker compose up -d
```

### DB環境構築
```
docker compose exec web rails db:create
docker compose exec web rails db:migrate
docker compose cp db/seeds.rb web:/rails/db/seeds.rb
docker compose exec web rails db:seed
```

### tailswindcssのインストール
```
docker compose run --rm web rails javascript:install:esbuild
docker compose run --rm web rails css:install:tailwind
docker compose down
docker compose build --no-cache
docker compose up -d
```

http://localhost:3000/books にアクセス

### テスト実行確認
- systemSpecができるかどうか確認
```
docker compose exec web bash -c "RAILS_ENV=test bundle exec rspec spec/system/"
```
errorが出ず、正常終了したら成功です

