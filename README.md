модель для сортировки любых данных в Yii2

Пример вызова
 
```
$productOffers = Offer::find()
    ->andWhere(['product_id'=>$productId])
    ->with([
        'store'
    ])->all();
$params = [
    'sort'=>substr_count($get['sort'], '-store') > 0 ? 'DESC' : 'ASC',
];
if(substr_count($get['sort'], 'price') > 0){
    $params['fields'] = 'price';
}
if(substr_count($get['sort'], 'rait') > 0){
    $params['fields'] = 'store.rating.avg_raiting';
}
if(substr_count($get['sort'], 'distance') > 0){
    $params['fields'] = 'store.nearestAddress';
    $params['callback'] = 'distance';
    $params['callbackValue'] = $point;
}

$offersSort = new SortModel(
    $params,
    $productOffers
);

$offers = $offersSort->sort();
```