# PlayerMovement
Here is the script from the yt tutorial

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Movement : MonoBehaviour
{
    private float horizontalInput;
    private float verticalInput;
    public float JumpForce;
    public bool isOnground;
    public float speed;
    private Rigidbody rb;

    private void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    // Update is called once per frame
    void Update()
    {
        horizontalInput = Input.GetAxis("Horizontal");
        verticalInput = Input.GetAxis("Vertical");

        transform.Translate(Vector3.right * speed * horizontalInput * Time.deltaTime);
        transform.Translate(Vector3.forward * speed * verticalInput * Time.deltaTime);

        if (Input.GetKeyDown(KeyCode.Space) && isOnground)
        {
            isOnground = false;
            rb.AddForce(Vector3.up * JumpForce, ForceMode.Impulse);  
        }
    }

    private void OnCollisionEnter(Collision collision)
    {
        if (collision.gameObject.CompareTag("Ground"))
        {
            isOnground = true;
        }    
    }

}
