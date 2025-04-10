
## Movimentação + Configuração de animações
```
using UnityEngine;

  

public class PlayerMovement : MonoBehaviour

{

    [Header("Movimentação")]

    public float moveSpeed = 10f;

    public Rigidbody2D rb;

  

    [Header("Animação")]

    public Animator animator;

  

    private Vector2 movement;

    private Vector2 lastMoveDir;

  

    void Update()

    {

        // Entrada do jogador (com normalize para manter velocidade constante na diagonal)

        movement = new Vector2(Input.GetAxisRaw("Horizontal"), Input.GetAxisRaw("Vertical")).normalized;

  

        // Atualiza estado da animação

        if (movement != Vector2.zero)

        {

            // Define se está se movendo

            animator.SetBool("IsMoving", true);

  

            // Determina a direção dominante para a animação

            if (Mathf.Abs(movement.x) > Mathf.Abs(movement.y))

            {

                // Horizontal domina

                animator.SetFloat("MoveX", movement.x);

                animator.SetFloat("MoveY", 0);

                lastMoveDir = new Vector2(Mathf.Sign(movement.x), 0);

            }

            else

            {

                // Vertical domina

                animator.SetFloat("MoveX", 0);

                animator.SetFloat("MoveY", movement.y);

                lastMoveDir = new Vector2(0, Mathf.Sign(movement.y));

            }

        }

        else

        {

            animator.SetBool("IsMoving", false);

  

            // Quando parado, mantém a última direção para o Idle correto

            animator.SetFloat("MoveX", lastMoveDir.x);

            animator.SetFloat("MoveY", lastMoveDir.y);

        }

    }

  

    void FixedUpdate()

    {

        // Movimento do personagem

        rb.linearVelocity = movement * moveSpeed;

    }

}
```




---
