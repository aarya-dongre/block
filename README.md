Practical 1: 
Circle > Add Rigidbody2d > Gravity 0 > Translation code > 
	public float speed = 5f; private Rigidbody2D rb2d; 
void Start() { rb2d = GetComponent<Rigidbody2D>(); } 
void Update() { 	float moveX = Input.GetAxis("Horizontal"); 
float moveY = Input.GetAxis("Vertical"); 
Vector2 movement = new Vector2(moveX, moveY); 
rb2d.linearVelocity = movement * speed; } }
Rotation code >
	public float speed = 200f; // Speed needs to be much higher for rotation (degrees per second) 
private Rigidbody2D rb2d; void Start() { rb2d = GetComponent<Rigidbody2D>(); } 
void Update() { float rotateInput = Input.GetAxis("Horizontal"); 
rb2d.angularVelocity = -rotateInput * speed; } }
Scaling code >
	public float speed = 5f; private Rigidbody2D rb2d; 
void Start() { rb2d = GetComponent<Rigidbody2D>(); } 
void Update() { 	float moveX = Input.GetAxis("Horizontal"); 
float moveY = Input.GetAxis("Vertical"); 
Vector2 movement = new Vector2(moveX, moveY); 
rb2d.linearVelocity = movement * speed; 
if (Input.GetKey(KeyCode.Q)) 
{ transform.localScale += Vector3.one * Time.deltaTime; } 
if (Input.GetKey(KeyCode.E)) 
{ transform.localScale -= Vector3.one * Time.deltaTime; 
if (transform.localScale.x < 0.1f) 
transform.localScale = new Vector3(0.1f, 0.1f, transform.localScale.z); } } }   
Practical 3:
Triangle > Rigidbody2d  > Gravity 0 > Jump code + Move + Color changing> 
	public float speed = 5f; public float jumpForce = 5f; 
public Color leftColor = Color.red; public Color rightColor = Color.blue; 
public Color idleColor = Color.white; private Rigidbody2D rb; 
private SpriteRenderer sr; 
void Start() { 	rb = GetComponent<Rigidbody2D>(); 
sr = GetComponent<SpriteRenderer>(); } 
void Update() { 	float moveX = Input.GetAxis("Horizontal");
rb.linearVelocity = new Vector2(moveX * speed, rb.linearVelocity.y); 
if (moveX > 0) { sr.color = rightColor; } 
else if (moveX < 0) { sr.color = leftColor; } 
else { sr.color = idleColor; } 
if (Input.GetKeyDown(KeyCode.Space)) 
{ rb.linearVelocity = new Vector2(rb.linearVelocity.x, jumpForce); } }}
Surface effector > Square > Box Collider (For a triangle as well) > Surface effector
No code only take triangle code
Practical 4 
UI > Canvas > Panel > TMP
Button code >
Public void sayHello() {Debug.Log( Hello )}
Button > On click > Select functions
Toggle code> 
public void UserValueChanged(bool value){ Debug.Log("Toggle Value Changed: "+ value); }
On value changed > Add function and all
Slider > Change min max value >
public void SliderValueChanged(float value) 
{ Debug.Log("Slider Value Changes: "+value); }
On value changed > Attach > do settings
Practical 5
Platform effector >
Square > Box Collider > Platform effector > Use collider mask > use one way > 
Triangle > Jump code 
Area effector > 
Square > Box Collider 2d > is trigger > used by effector > Area Effector 2d > collider mask
Buyoncy effector >
Square > Box Collider > is trigger > used by effector > Buyoncy effector > collider mask > density:3 > surface level : 0.52
Audio Listners >Square > Audio Source > Audio Resrouce > 
using UnityEngine; 
[RequireComponent(typeof(AudioSource))] 
public class audio : MonoBehaviour 
{ private AudioSource audioSrc; 
void Start() { audioSrc = GetComponent<AudioSource>(); 
if (audioSrc == null) { Debug.LogError("AudioSource not found on Wind Zone!"); } 
else { audioSrc= GetComponent<AudioSource>(); 
if (audioSrc == null) { Debug.LogError("AudioSource not found on Wind Zone!"); } 
else { audioSrc.loop = true; audioSrc.playOnAwake = false; } } 
private void OnTriggerEnter2D(Collider2D other) 
{ if (other.CompareTag("Player")) 
{ if (!audioSrc.isPlaying) { audioSrc.Play(); } } }
private void OnTriggerExit2D(Collider2D other) 
{ if (other.CompareTag("Player")) { audioSrc.Stop(); } } }
Practical 6
UI >Button > Give name and all > 
using UnityEngine.SceneManagement; 
public class parc6_1 : MonoBehaviour 
{ public void LoadScene() 
{ SceneManager.LoadScene("prac6"); } }
On click > Drag and Drop button with script settings do 
File > Build Profiles > scene list > Add Open Scenes > Recent scene select 
Complex/Asynchronous scene > Same setup but different script >
Using System.Collections;
public void LoadSceneAsyncButton() 
{ StartCoroutine(LoadAsync()); } 
IEnumerator LoadAsync() { AsyncOperation operation = 
SceneManager.LoadSceneAsync("prac6"); 
while (!operation.isDone) { Debug.Log(operation.progress*100 + "%"); yield return null; }
On Click change settings and all 
Additive Scene > Same setup
using UnityEngine.SceneManagement;
public void LoadSceneAdd() 
{ SceneManager.LoadScene("prac6",LoadSceneMode.Additive); }
On click change settings and all 
Unload Scene > same setup >
New scene give > 
using UnityEngine.SceneManagement;
public void UnloadScene() 
{ SceneManager.LoadScene("MainScene"); 
SceneManager.UnloadSceneAsync("prac6"); }
Practical 7
Range Checker 
3D > cube > sphere > 
Cube player > script >
[serializefield] private target transform;[serializefield] private float range=5;
void update()
{	float distance =Vector3.Distance(transform.position, target.position);
	bool inrange=distance<=range;
	if(inrange){print("Target in range")}
	else{		print("Target is not in range")}}	
Target in script inspector > Sphere
Angle Checker > Same setup >
using UnityEngine;
public class TargetDistance : Monobehaviour 
{	[SerializeField] private Transform object;
	void Update()
{		float angle = Vector3.Angle(transform.forward, target.position - transform.position);
        Debug.Log("Angle: " + angle);	}}
Target > Sphere > 
Practical 8
3d > Plane > 2 Capsules > Cube  > Add colour by > Create > Materials
Goal > sphere collider > is trigger > 
Player > rigid body > use gravity no > Constraints > Freeze Rotaiton all tick >
Ai > Nav Mesh Agent > 
Empty object > NavMesh name > Navmesh surface component > Bake
Player:
public float speed = 5f; Rigidbody2D rb; 
void Start() { rb=GetComponent<Rigidbody2D>(); } 
void FixedUpdate() { float horizontal = Input.GetAxis("Horizontal"); 
float vertical = Input.GetAxis("Vertical"); 
Vector3 move = new Vector3(horizontal,0, vertical) * speed; 
rb.linearVelocity = new Vector3(move.x, rb.linearVelocity.y, move.z); }
Ai >
using UnityEngine.AI;
public Transform target; public float speed = 3.5f; private NavMeshAgent agent; 
void Start(){ agent = GetComponent<NavMeshAgent>(); agent.speed = speed; } 
void Update() { if (target != null) { agent.SetDestination(target.position); }}
Goal > 
public class GOAL : MonoBehaviour 
{ private void OnTriggerEnter(Collider other) 
{ if(other.CompareTag("Player")) { Debug.Log("You Win!"); Time.timeScale=0; } 
else if(other.CompareTag("Enemy")) { Debug.Log("AI Wins!"); Time.timeScale=0; } }
GameManager >
public GameObject player; public GameObject ai; public GameObject goal; 
void Update() {float playerDistance = Vector3.Distance(player.transform.position, goal.transform.position); 
float aiDistance = Vector3.Distance(ai.transform.position, goal.transform.position); 
if(playerDistance < 1.0f) { Debug.Log("You Win!"); Time.timeScale=0; } 
else if(aiDistance < 1.0f){ Debug.Log("AI Wins!"); QuitGame(); } } 
void QuitGame() { Application.Quit(); UnityEditor.EditorApplication.isPlaying = false; }
Make settings in all scripts and add tags to enemy and player 
Chase game > same setup remove goal 
Player > 
public float speed=5f; 
void Update() { float h= Input.GetAxis("Horizontal");
float v= Input.GetAxis("Vertical"); Vector3 move=new Vector3(h,0.0f,v); 
transform.Translate(move*speed*Time.deltaTime, Space.World); }
Ai >
using UnityEngine.AI;
public Transform player; private NavMeshAgent agent; public float detectionRange=5.0f; 
void Start() { agent=GetComponent<NavMeshAgent>(); } 
void Update() {if(Vector3.Distance(transform.position, player.position) < detectionRange) { agent.SetDestination(player.position); Debug.Log("AI is Chasing "); 
float distanceToPlayer = Vector3.Distance(transform.position, player.position); 
Debug.Log("Distance to Player: " + distanceToPlayer); 
if (distanceToPlayer < 0.5f) { Debug.Log("AI Wins!"); StopChasing(); } }} 
void StopChasing() { Application.Quit(); UnityEditor.EditorApplication.isPlaying = false; }
Capsule collider > is trigger true > for all and put target in ai > 
Practical 9
    public Animator animator;
    void Start() {animator = GetComponent<Animator>()}
    void Update()    {      animator.SetBool("run", Input.GetKeyDown(KeyCode.W));
        animator.SetBool("walk", Input.GetKeyDown(KeyCode.E));}}


