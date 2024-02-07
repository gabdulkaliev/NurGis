# NurGis - карта с отмеченными интересными местами
Простая программа на Java. показывающая интересные места в городе Павлодар (есть возможность сортировки)
Ниже основной код главной страницы
```java
public class MainActivity extends FragmentActivity implements OnMapReadyCallback {

    private GoogleMap mMap; // Карта
    private TextView textView; // Текстовый компонет

    private String markerTitle = ""; // Название выбранного маркера
    private String markerFileName = ""; // Имя файла с подробными данными выбранного маркера

    private final int SITYSCALE = 17; // Масштаб для отображения карты
    static final LatLng startMarker = new LatLng(52.272613, 76.971165); // Начальный маркер
    //...

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    @Override
    public void onMapReady(GoogleMap googleMap) {
        mMap = googleMap;

        // Обычный тип карты
        mMap.setMapType(GoogleMap.MAP_TYPE_NORMAL);
        mMap.setMapStyle(MapStyleOptions.loadRawResourceStyle(MainActivity.this, R.raw.night_mode));

        // Добавление маркера на карту с текстом
        mMap.addMarker(new MarkerOptions().position(startMarker).title((getString(R.string.startMarker_title))));

        //...
        // Переход просмотра на карте на нужный маркер c зумом
        mMap.moveCamera(CameraUpdateFactory.newLatLngZoom(startMarker, SITYSCALE));

        // Инициализация стартового маркера
        onMarkerClick(getString(R.string.startMarker_id));

        // Обработчик нажатия на маркеры карты
        mMap.setOnMarkerClickListener(new GoogleMap.OnMarkerClickListener() {
            @Override
            public boolean onMarkerClick(Marker marker) {
                marker.showInfoWindow();
                MainActivity.this.onMarkerClick(marker.getId());
                return true;
            }
        });
    }
```
![one]()
