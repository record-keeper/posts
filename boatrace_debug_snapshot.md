# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-17T15:00:02.408858+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×55 (24h) → ログ/DB確認

### 検出された問題
- 🔴 PSI_DRIFT_DETECTED×55 (24h)
- 🟡 FINAL_MISSING×43 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×11 (24h)
- 🔴 CALIBRATION_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-17T15:00:08]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-17T15:00:08]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×106  [2026-09-17T14:05:06]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×53  [2026-09-17T14:05:06]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×53  [2026-09-17T14:05:06]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CIRCUIT_BREAKER_TRIP  ×17  [2026-09-17T12:11:29]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×9  [2026-09-17T10:55:57]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-17T06:00:22]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=77<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-17T06:00:22]
- key: `INSUFFICIENT_SAMPLE|S00: n=178<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-09-17T06:00:22]
- key: `ORPHAN_SCAN|173 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-17T06:00:22]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=176<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-17T06:00:22]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1314 actual=0.0000 gap=+0.1314`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-17T06:00:22]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1783 actual=0.3333 gap=-0.1550`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-17T06:00:22]
- key: `ROI_STAT|S00: n=178 hit%=27.5% hit_CI[Bonf]=[19.0,38.0]% ROI=0.96 ROI_boot95=[0.69,1.28]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-17T06:00:22]
- key: `ROI_STAT|S01_NAKAANA1: n=176 hit%=23.9% hit_CI[Bonf]=[15.9,34.2]% ROI=0.74 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-17T06:00:22]
- key: `ROI_STAT|S02_TETSUBAN: n=77 hit%=35.1% hit_CI[Bonf]=[21.5,51.5]% ROI=0.63 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-17T06:00:22]
- key: `DRIFT_BUCKET|drift ≤-30%: n=32 hit%=28.1% ROI=0.85 (コスト 9,200/回収 7,850)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-17T06:00:22]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=44 hit%=25.0% ROI=0.73 (コスト 10,300/回収 7,540)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-17T06:00:22]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=86 hit%=22.1% ROI=0.85 (コスト 19,800/回収 16,890)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-17T06:00:22]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=47 hit%=21.3% ROI=0.43 (コスト 10,300/回収 4,480)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 13.46MB / last modified 2026-09-17T15:00:08.435900+09:00

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
4:58:45,534 [INFO] run_cycle: fetched 16/9 [final]: 153 combos
2026-09-17 14:58:46,174 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-17 14:59:04,677 [INFO] run_cycle: === run_cycle 14:59:04 ===
2026-09-17 14:59:04,677 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-17 14:59:04,677 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-17 14:59:04,750 [INFO] predictor: Models loaded OK
2026-09-17 14:59:15,857 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=9&jcd=16&hd=20260917: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-09-17 14:59:27,427 [INFO] scraper: odds3t: 120/120 parsed
2026-09-17 14:59:28,676 [INFO] scraper: odds3f: 20/20 parsed
2026-09-17 14:59:29,956 [INFO] scraper: odds2t: 30/30 parsed
2026-09-17 14:59:29,958 [INFO] scraper: odds2f: 12/15 parsed
2026-09-17 14:59:31,041 [INFO] scraper: odds_win: 3/6 parsed
2026-09-17 14:59:31,041 [INFO] scraper: fetch_race 16/9: boats=6 odds=185/191
2026-09-17 14:59:31,052 [INFO] predictor: CALIBRATION_MODE=on
2026-09-17 14:59:31,052 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-09-17 14:59:31,060 [INFO] run_cycle: fetched 16/9 [final]: 153 combos
2026-09-17 14:59:34,868 [INFO] scraper: odds3t: 120/120 parsed
2026-09-17 14:59:35,957 [INFO] scraper: odds3f: 20/20 parsed
2026-09-17 14:59:37,045 [INFO] scraper: odds2t: 30/30 parsed
2026-09-17 14:59:37,046 [INFO] scraper: odds2f: 12/15 parsed
2026-09-17 14:59:38,201 [INFO] scraper: odds_win: 4/6 parsed
2026-09-17 14:59:38,201 [INFO] scraper: fetch_race 09/10: boats=6 odds=186/191
2026-09-17 14:59:38,204 [INFO] predictor: CALIBRATION_MODE=on
2026-09-17 14:59:38,204 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-09-17 14:59:38,208 [INFO] run_cycle: fetched 09/10 [scan]: 154 combos
2026-09-17 14:59:38,533 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 78
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 78
  }
]
```

## Phase別通知記録 (24h)
{'final': 33, 'result': 16, 'scan': 29}

## アラート件数 (24h・種類別)
```
  PSI_DRIFT_DETECTED: 55
  FINAL_MISSING: 43
  ANOMALY_SCRAPER_FAILURE_BURST: 35
  CIRCUIT_BREAKER_NO_ACTION: 34
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_TRIP: 11
  ANOMALY_BET_VOLUME_SPIKE: 3
  CALIBRATION_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 37 | 9 | 11,100 | 8,130 | -2,970 | 0.732 |
| S01_NAKAANA1 | 31 | 9 | 6,200 | 5,760 | -440 | 0.929 |
| S02_TETSUBAN | 16 | 8 | 3,200 | 3,100 | -100 | 0.969 |

## 直近アラート (24h・新しい順)
```
[14:53:45] FINAL_MISSING: {"deadline": "2026-09-17T11:23:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091704021123", "sid": "S00"}
[14:48:21] FINAL_MISSING: {"deadline": "2026-09-17T10:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091714051016", "sid": "S00"}
[14:26:21] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 340, "n_recent": 84, "psi": 0.643}
[14:23:32] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 341, "n_recent": 84, "psi": 0.642}
[14:22:36] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 342, "n_recent": 84, "psi": 0.649}
[14:07:51] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 343, "n_recent": 84, "psi": 0.656}
[14:06:04] FINAL_MISSING: {"deadline": "2026-09-17T13:36:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091708071336", "sid": "S00"}
[14:03:45] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[14:03:44] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[14:03:44] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
```

## 本日残レース: 77件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 103件 締切済
- 通知発射: scan=14 nid / final=17 nid / result=8 nid
- predictions: 8 / うち結果DB記録済: 8
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 057R | win | 1 | 0.5174 | 2.5 | 1.29 | 200 | scan=- drift=- | 13:27:21 |
| S02_TETSUBAN | 117R | win | 1 | 0.5612 | 2.0 | 1.12 | 200 | scan=- drift=- | 13:19:20 |
| S00 | 165R | win | 1 | 0.5891 | 4.1 | 2.42 | 300 | scan=- drift=- | 12:49:21 |
| S00 | 222R | win | 1 | 0.5174 | 7.5 | 3.88 | 300 | scan=7.5 drift=+0.0% | 12:11:20 |
| S00 | 114R | win | 1 | 0.5334 | 13.5 | 7.20 | 300 | scan=- drift=- | 11:47:30 |
| S00 | 113R | win | 1 | 0.0754 | 5.6 | 0.42 | 300 | scan=7.5 drift=-25.3% | 11:19:18 |
| S02_TETSUBAN | 092R | win | 1 | 0.5460 | 2.2 | 1.20 | 200 | scan=2.0 drift=+10.0% | 10:58:20 |
| S01_NAKAANA1 | 234R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=- drift=- | 09:59:32 |
| S02_TETSUBAN | 074R | win | 1 | 0.5518 | 2.0 | 1.10 | 200 | scan=- drift=- | 16:39:19 |
| S01_NAKAANA1 | 124R | win | 1 | 0.4111 | 4.0 | 1.64 | 200 | scan=- drift=- | 16:32:45 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 51 | +6.9% | -80.2% | +119.5% | 12 | 2 | 30 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 405.2s |
| **Latency** (scan→final max) | 615.3s |
| **Traffic** (notifications 24h) | 78 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 424 | 0.4777 | 0.2712 | +0.2064 | 🟡+43% | 0.2416 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 175 | 0.4390 | 0.2571 | 0.2301 | 🔴-0.20 | 0.826 |
| S01_NAKAANA1 | win | 170 | 0.4861 | 0.2353 | 0.2433 | 🔴-0.35 | 0.658 |
| S02_TETSUBAN | win | 79 | 0.5451 | 0.3797 | 0.2633 | 🔴-0.12 | 0.714 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1314 | 0.0000 | 🔴+0.1314 |
| 0.15-0.20 | 6 | 0.1783 | 0.3333 | 🔴-0.1550 |
| 0.20-0.30 | 6 | 0.2221 | 0.0000 | 🔴+0.2221 |
| 0.30-0.50 | 144 | 0.4086 | 0.2153 | 🔴+0.1933 |
| 0.50+ | 257 | 0.5453 | 0.3113 | 🔴+0.2340 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 142 | 0.777 |
| win | <5.0 | ✅learned | 254 | 0.757 |
| win | <10.0 | ✅learned | 122 | 0.466 |
| win | <20.0 | ✅learned | 33 | 0.234 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-09-17T15:00:02.408858+09:00_