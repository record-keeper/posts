# ClaudeDebug スナップショット

## 🟢 現状: GREEN

**生成**: 2026-04-22T07:40:01.663648+09:00

### 次に取るべきアクション
> 特になし。運用継続。

### 問題なし、運用継続してOK。

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### ℹ️ CALIBRATION_LIVE  ×1  [2026-04-22T06:00:07]
- key: `CALIBRATION_LIVE|decile 0.50+: n=6 pred=0.5304 actual=0.1667 gap=+0.3638`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 PAYOUT_RATIO_WEIRD  ×1  [2026-04-22T06:00:06]
- key: `PAYOUT_RATIO_WEIRD|pid=759 bet=300 odds=4.0 payout=1980 ratio=1.65`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×8  [2026-04-21T23:52:05]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### ℹ️ CODE_AUDIT_RANK_ARROW_INCONSISTENT_HISTORICAL  ×3  [2026-04-21T21:00:03]
- key: `CODE_AUDIT_RANK_ARROW_INCONSISTENT_HISTORICAL|scan title に 🆙 ある件 7件（履歴、修正前分）`
- **FIX**: 過去 scan title の 🆙 履歴。修正後の scan が入ると消える。直近1時間で検出→要調査

### 🟡 CODE_AUDIT_DEAD_CODE_BUILD_EMBED_CALLED  ×3  [2026-04-21T21:00:03]
- key: `CODE_AUDIT_DEAD_CODE_BUILD_EMBED_CALLED|1 件 build_embed 呼び出し（strategy['bet_type'] KeyError risk）`
- **FIX**: 非推奨 notifier.build_embed() 呼出（strategy['bet_type'] KeyError risk）。build_strategy_embed_v2 に移行


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `149bfa9ecc7e714a646f5a33d43fea95`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 1.09MB / last modified 2026-04-22T07:30:03.143553+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
06 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-21 23:55:06,007 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-21 23:55:06,088 [INFO] predictor: Models loaded OK
2026-04-21 23:55:06,097 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-21 23:56:05,968 [INFO] run_cycle: === run_cycle 23:56:05 ===
2026-04-21 23:56:05,968 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-21 23:56:05,968 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-21 23:56:06,014 [INFO] predictor: Models loaded OK
2026-04-21 23:56:06,019 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-21 23:57:05,696 [INFO] run_cycle: === run_cycle 23:57:05 ===
2026-04-21 23:57:05,696 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-21 23:57:05,698 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-21 23:57:05,775 [INFO] predictor: Models loaded OK
2026-04-21 23:57:05,780 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-21 23:58:05,758 [INFO] run_cycle: === run_cycle 23:58:05 ===
2026-04-21 23:58:05,758 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-21 23:58:05,758 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-21 23:58:05,810 [INFO] predictor: Models loaded OK
2026-04-21 23:58:05,814 [INFO] run_cycle: run_cycle done: 0 notifications
2026-04-21 23:59:05,474 [INFO] run_cycle: === run_cycle 23:59:05 ===
2026-04-21 23:59:05,474 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-04-21 23:59:05,474 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-04-21 23:59:05,537 [INFO] predictor: Models loaded OK
2026-04-21 23:59:05,543 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 29
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 29
  }
]
```

## Phase別通知記録 (24h)
{'final': 10, 'result': 12, 'scan': 7}

## アラート件数 (24h・種類別)
```
  ANOMALY_BET_VOLUME_SPIKE: 3
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 12 | 2 | 3,600 | 3,120 | -480 | 0.867 |

## 直近アラート (24h・新しい順)
```
[23:00:08] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 2, "baseline_n_days": 3, "baseline_stdev": 1.7, "hour": 23, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 6, "z_score": 2.31}
[22:00:09] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 2, "baseline_n_days": 3, "baseline_stdev": 1.7, "hour": 22, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 6, "z_score": 2.31}
[21:50:51] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 2, "baseline_n_days": 3, "baseline_stdev": 1.7, "hour": 21, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 6, "z_score": 2.31}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 0件 登録 / 0件 締切済
- 通知発射: scan=0 nid / final=0 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 154R | win | 1 | 0.4111 | 4.0 | 1.64 | 300 | scan=- drift=- | 16:48:45 |
| S00 | 243R | win | 1 | 0.5174 | 4.8 | 2.48 | 300 | scan=5.8 drift=-17.2% | 16:04:20 |
| S00 | 225R | win | 1 | 0.5719 | 8.5 | 4.86 | 300 | scan=7.5 drift=+13.3% | 14:22:21 |
| S00 | 056R | win | 1 | 0.5035 | 6.5 | 3.27 | 300 | scan=6.6 drift=-1.5% | 13:58:20 |
| S00 | 186R | win | 1 | 0.5057 | 7.0 | 3.54 | 300 | scan=- drift=- | 10:45:20 |
| S00 | 185R | win | 1 | 0.4694 | 4.0 | 1.88 | 300 | scan=- drift=- | 10:15:20 |
| S00 | 073R | win | 1 | 0.5477 | 5.1 | 2.79 | 300 | scan=- drift=- | 16:09:21 |
| S00 | 223R | win | 1 | 0.3561 | 41.2 | 14.67 | 300 | scan=36.7 drift=+12.3% | 13:26:31 |
| S00 | 187R | win | 1 | 0.1608 | 6.9 | 1.11 | 300 | scan=5.3 drift=+30.2% | 11:25:20 |
| S00 | 186R | win | 1 | 0.5364 | 5.1 | 2.74 | 300 | scan=- drift=- | 10:53:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 5 | +7.4% | -17.2% | +30.2% | 1 | 0 | 4 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 442.7s |
| **Latency** (scan→final max) | 622.3s |
| **Traffic** (notifications 24h) | 29 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 12 | 0.4567 | 0.1667 | +0.2900 | 🔴+64% | 0.2269 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 12 | 0.4567 | 0.1667 | 0.2269 | 🔴-0.63 | 0.867 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 5 | 0.4273 | 0.2000 | 🔴+0.2273 |
| 0.50+ | 6 | 0.5304 | 0.1667 | 🔴+0.3638 |

## Settlement Ratio データ品質

- 学習済み: 0バンド / fallback: 16バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ⚠️fallback | 0 | 0.4 |
| win | <5.0 | ⚠️fallback | 1 | 0.35 |
| win | <10.0 | ⚠️fallback | 1 | 0.32 |
| win | <20.0 | ⚠️fallback | 0 | 0.22 |
| win | <50.0 | ⚠️fallback | 0 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-04-22T07:40:01.663648+09:00_