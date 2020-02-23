# view-binding-sample

## Android Studio
Android Studio 4.0 Canary 9

## Kotlin
Kotlin 1.3.61

## Tips
### Enable view binding
```kotlin:build.gradle.kts
    buildFeatures {
        viewBinding = true
    }
```

### Activity
```kotlin:MainActivity.kt
class MainActivity : AppCompatActivity(R.layout.main_activity) {

    private val binding: MainActivityBinding by lazy {
        MainActivityBinding.bind(findViewById<ViewGroup>(android.R.id.content)[0]) }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        val navController = findNavController(R.id.nav_host_fragment)
        val appBarConfiguration = AppBarConfiguration(setOf(
                R.id.navigation_home, R.id.navigation_dashboard, R.id.navigation_notifications))
        setupActionBarWithNavController(navController, appBarConfiguration)
        binding.navView.setupWithNavController(navController)
    }
}
```

### Fragment
```kotlin:MainActivity.kt
class DashboardFragment : Fragment() {
    
    private lateinit var binding: DashboardFragmentBinding
    
    override fun onCreateView(
        inflater: LayoutInflater,
        container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        binding = DashboardFragmentBinding.inflate(layoutInflater, container, false)
        dashboardViewModel.text.observe(viewLifecycleOwner, Observer {
            binding.textDashboard.text = it
        })
        return binding.root
    }
}
```