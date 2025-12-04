# 09

① メニュー一覧を取得（GET /menus）
■ Request（スマホ → サーバー）
GET /menus
■ Response（サーバー → スマホ）
[
  {
    "menu_id": 1,
    "name": "唐揚げ定食",
    "price": 650,
    "image_url": "/static/img/karaage.jpg"
  },
  {
    "menu_id": 2,
    "name": "カレーライス",
    "price": 500,
    "image_url": "/static/img/curry.jpg"
  }
]
② メニュー詳細を取得（GET /menus/<menu_id>）
■ Request
GET /menus/1
■ Response
{
  "menu_id": 1,
  "name": "唐揚げ定食",
  "price": 650,
  "description": "揚げたての唐揚げとご飯セット",
  "image_url": "/static/img/karaage.jpg"
}
③ カートに入れる（POST /cart）
■ Request
スマホが送るデータ（どのメニューを何個入れるか）
{
  "menu_id": 1,
  "quantity": 2
}
■ Response
サーバーが返す（カートに追加できた）
{
  "cart_item_id": 15,
  "message": "Item added to cart",
  "menu_id": 1,
  "quantity": 2
}
④ カートの項目を削除（DELETE /cart/<cart_item_id>）
■ Request
DELETE /cart/15
■ Response
{
  "message": "Cart item deleted",
  "deleted_id": 15
}
⑤ カート内を一括注文（POST /orders）
■ Request
スマホ側が送る（カート内を注文として送信）
{
  "cart_items": [
    { "menu_id": 1, "quantity": 2 },
    { "menu_id": 3, "quantity": 1 }
  ]
}
■ Response
サーバーが返す（注文確定）
{
  "order_id": 3021,
  "status": "cooking",
  "wait_time_minutes": 10,
  "message": "Order accepted"
}
⑥ 注文ステータスの取得（GET /orders/<id>/status）
■ Request
GET /orders/3021/status
■ Response
{
  "order_id": 3021,
  "status": "cooking",
  "message": "Your order is being prepared",
  "pickup_number": 89
}
⑦ 受け取り可に変更（PUT /orders/<id>/status）
■ Request
（厨房側が行う想定だけど課題ではスマホでもOK）
{
  "status": "ready"
}
■ Response
{
  "order_id": 3021,
  "status": "ready",
  "message": "Order is ready for pickup"
}
⑧ 受け取り済みに変更（PUT /orders/<id>/status）
■ Request
{
  "status": "picked_up"
}
■ Response
{
  "order_id": 3021,
  "status": "picked_up",
  "message": "Order pickup completed"
}
✔️ワークシートにそのまま載せられる完成版！
もし docx か md の提出用ひな形が必要なら
この JSON を入れたレポートとして作ってあげるよ。
作る？
